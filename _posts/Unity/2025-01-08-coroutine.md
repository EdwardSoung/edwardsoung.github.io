---
layout: post
title: Coroutine이란?
author: Hyunwoo Soung
categories: unity
tags:
  - Unity
  - coroutine
image: algorithm.jpg
published: true
---

#### 📝기반내용

---

코루틴은 유니티에만 사용하는 요소는 아닙니다.

> 코루틴이란?  
> 실행의 지연과 재개를 허용함으로써, **비선점형 멀티태스킹**을 위한 **서브 루틴**을 일반화한 컴퓨터 프로그램 구성요소

원론적 의미의 코루틴은 자세하게 설명해놓은 부분을 찾아서, 링크로 대체하겠습니다. [\[코루틴에 대하여\]](https://dev.gmarket.com/82 "[코루틴에 대하여]")

비선점형 멀티태스킹을 간단하게 설명하면, CPU를 사용중인 쓰레드를 OS가 강제로 뺏어올 수 없는(선점할 수 없는) 형태의 멀티태스킹을 말합니다. 즉, 현재 쓰레드의 사용이 끝나야만 OS에서 다른 쓰레드를 CPU에 할당할 수 있습니다.

**코루틴은 병행성은 제공하지만, 병렬성은 제공하지 않습니다.**

> 병행성(=동시성, Concurrency) : 논리적으로 병렬로 작업이 실행되는 것처럼 보이는 것  
> 병렬성(Parallelism) : 물리적으로 병렬로 작업이 실행되는 것

#### 💡유니티에서의 코루틴

---

유니티는 기본적으로는 단일 쓰레드 기반(비선점형 멀티태스킹과 유사환경)으로 코루틴을 사용하여 병행성을 확보합니다.  
👉  .NET에서 멀티 쓰레드를 지원하기도 하고 Unity에서 Job System도 만들었기 때문에 멀티쓰레드 사용 자체가 불가능 한 것은 아닙니다.

1\. 특징

-   IEnumerator를 반환하는 형태의 메서드입니다.
-   실제로 동기식이지만 지연과 재개를 허용하기 때문에 비동기 처럼 동작하는 것으로 보입니다.

```
private IEnumerator MyCoroutine()
{
	//무한반복일 경우 Update와 유사한 동작을 한다.
	while(true)
    	{
    		//매 프레임 반복 호출
    		yield return null;
    	}
	yield break;
}
```

2\. 동작

-   유니티에서 Update 호출이 완료된 후 호출됩니다.(LateUpdate 호출 전)
-   유니티에서 StartCoroutine을 통해 동작할 IEnumerator들을 보관 후 순차 실행합니다.

3\. 조건

-   유니티에서 코루틴 시작을 관리하기 때문에 MonoBehavior를 상속받은 객체에서만 실행됩니다.
-   코루틴이 동작하는 객체가 활성화되어 있어야만 동작합니다.

#### 📝실행의 지연과 재개

---

> IEnumerator는 Current(), MoveNext(), Reset()로 이루어짐  
> Current : 현재 반환값  
> MoveNext : 열거자 내용 실행  
> Reset : Current를 null로 초기화시켜 처음부터 실행

👉 열거자 구조를 사용하여 **현재 실행 위치를 저장**하고, 다음 Update 주기에 저장된 위치부터 **실행을 재개**합니다.

> **yield return**  
> yield return문에 도달하면 뒤의 값을 반환하고 현재 위치를 저장한다. [\[MicroSoft - Iterator\]](https://learn.microsoft.com/ko-kr/dotnet/csharp/programming-guide/concepts/iterators)

1\. yield return null

반환값이 null이기 때문에 현재 위치만 저장하고 빠져나옵니다.

2\. yield return (IEnumerator 반환메서드)

\- 다른 열거형을 반환하는 경우 해당 열거형을 실행하고 위치를 저장합니다.

```
private IEnumerator CustomCoroutine()
{
    yield return CustomWaitForSeconds(1f);
}

//유니티에서 제공하는 WaitForSeconds와 동일한 동작
private IEnumerator CustomWaitForSeconds(float time)
{
    float timer = 0;
    while(true)
    {
        timer += Time.deltaTime;
        if(timer >= time)
        {
            yield break;
        }
        else
        {
            yield return null;
        }
    }
}
```

👉 CustomCoroutine에서 yield return을 만나면, 해당 위치가 저장되고 CustomWaitForSeconds가 실행

👉 CustomWaitForSeconds에서도 yield return이 있기 때문에 실행되면 저장된 위치부터 실행

3\. yield break

Enumerator에서 리턴을 중지하고 빠져나옵니다.

#### 📝간단 정리

-   열거형을 yield return을 만나면 반환하고, 다시 해당 위치에서 실행하는 반복 형태라고 보면 될 것 같습니다.
-   yield break를 만나면 반복문의 break와 같이 바로 빠져나갑니다.