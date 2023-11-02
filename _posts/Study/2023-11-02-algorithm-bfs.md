---
layout: post
title: Algorithm - BFS[Breadth-First Serch]
author: Hyunwoo Soung
categories: study
tags:
  - Sort
  - Algorithm
image: algorithm.jpg
published: true
---

## BFS[너비 우선 탐색]   
   
### 1. 너비 우선 탐색이란  
#### 루트 노드(혹은 다른 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방법  

시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법이다.  
즉, 깊게(deep) 탐색하기 전에 넓게(wide) 탐색하는 것이다.  
<br><br>

**사용하는 경우: 두 노드 사이의 최단 경로 혹은 임의의 경로를 찾고 싶을 때 이 방법을 선택한다.** 
- 깊이 우선 탐색의 경우 - 모든 친구 관계를 다 살펴봐야 할지도 모른다.  
- 너비 우선 탐색의 경우 - Ash와 가까운 관계부터 탐색  
- 너비 우선 탐색(BFS)이 깊이 우선 탐색(DFS)보다 좀 더 복잡하다.  
<br><br>

#### 너비 우선 탐색(BFS)의 특징  
- 직관적이지 않은 면이 있다.  
- BFS는 시작 노드에서 시작해서 거리에 따라 단계별로 탐색한다고 볼 수 있다.  
- BFS는 재귀적으로 동작하지 않는다.  
- 이 알고리즘을 구현할 때 가장 큰 차이점은, 그래프 탐색의 경우 어떤 노드를 방문했었는지 여부를 반드시 검사 해야 한다는 것이다.  
- 이를 검사하지 않을 경우 무한루프에 빠질 위험이 있다.  
- BFS는 방문한 노드들을 차례로 저장한 후 꺼낼 수 있는 자료 구조인 큐(Queue)를 사용한다.  
- 즉, 선입선출(FIFO) 원칙으로 탐색, 일반적으로 큐를 이용해서 반복적 형태로 구현하는 것이 가장 잘 동작한다.  
<br><br>

+ Pseudo code   

 ```
void search(Node root) 
{
    Queue queue = new Queue();
    root.marked = true; // (방문한 노드 체크)
    queue.enqueue(root); // 1-1. 큐의 끝에 추가

    // 3. 큐가 소진될 때까지 계속한다.
    while (!queue.isEmpty()) {
      Node r = queue.dequeue(); // 큐의 앞에서 노드 추출
      visit(r); // 2-1. 큐에서 추출한 노드 방문
      // 2-2. 큐에서 꺼낸 노드와 인접한 노드들을 모두 차례로 방문한다.
      foreach (Node n in r.adjacent) {
        if (n.marked == false) {
          n.marked = true; // (방문한 노드 체크)
          queue.enqueue(n); // 2-3. 큐의 끝에 추가
        }
      }
    }
}
 ```

### 너비 우선 탐색(BFS)의 시간 복잡도  
   
인접 리스트로 표현된 그래프: O(N+E)  
인접 행렬로 표현된 그래프: O(N^2)  
깊이 우선 탐색(DFS)과 마찬가지로 그래프 내에 적은 숫자의 간선만을 가지는 희소 그래프(Sparse Graph) 의 경우 인접 행렬보다 인접 리스트를 사용하는 것이 유리하다.  