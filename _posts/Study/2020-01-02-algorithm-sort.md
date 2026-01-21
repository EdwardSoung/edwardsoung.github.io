
## 기본 정렬 알고리즘
> <b><span style="color:black">평균 소요시간이 $$\Theta(n^2)$$ 인 정렬 알고리즘</span></b>  

### 1. Selection Sort(선택 정렬)
> <b><span style="color:black">배열에서 가장 큰 수를 찾아 배열 마지막 자리와 바꾸는 형태의 정렬</span></b>
   
+ Pseudo code   

```
SelectionSort(A[], n)
{
  for last <- n downto 2
  {
    k <- TheLargest(A, last);
    A[k] <-> A[last];
  }
}

TheLargest(A[], last)
{
  largest <- 1;
  for i <- 2 to last
    if(A[i] > A[largest]) then largest <- i;
    return largest;
}
```
   

- C# 코드 구현   

```cs
public int[] SelectionSort(int[] arr)
{

}

```
### 2. Bubble Sort(버블 정렬)
> <b><span style="color:black">배열의 왼쪽부터 이웃한 수를 비교하며 바꾸는 형태의 정렬</span></b>
   
- Pseudo Code

```
BubbleSort(A[], n)
{
  for last <- n downto 2
    for i <- 1 to last - 1
      if(A[i] > A[i + 1]) then A[i] <-> A[i + 1];
}
```   
   
- C# 코드 구현   

```cs
public int[] BubbleSort(int[] arr)
{

}
```

위의 경우 이미 정렬된 상태여도 끝까지 무의미한 순환을 계속 한다.  

- 개선된 Bubble Sort Pseudo Code   
   
```
BubbleSort(A[], n)
{
  for last <- n downto 2
  {
    sorted <- TRUE;
    for i <- 1 to last - 1
    {
      if(A[i] > A[i + 1]) then
      {
        A[i] <-> A[i + 1];
        sorted <- FALSE;
      }         
    }
    if(sorted == TRUE) then return;
  } 
}
```   
   
- C# 코드 구현   

```cs
public int[] BubbleSort(int[] arr)
{

}
```

for문을 돌면서 중간에 한 번이라도 A[i] <-> A[i + 1]의 교환이 일어나면 sorted를 FALSE로 변경하여 준다.   
-> 이미 정렬된 경우 sorted == TURE이므로 for문을 한번만 순환하고 반환하게 된다.

### 3. Insertion Sort(삽입 정렬)
> <b><span style="color:black">이미 정렬되어 있는 i개짜리 배열에 하나의 원소를 더하여 정렬된 i + 1개짜리 배열을 만드는 형태의 정렬</span></b>   
   
- Pseudo Code   

```
InsertionSort(A[], n)
{
  for i <- 1 to n
  {
    loc <- (i - 1);
    newItem <- A[i];
    while(loc >= 1 and newItem < A[loc])
    {
      A[loc + 1] <- A[loc];
      loc--;
    }
    A[loc + 1] <- newItem;
  }
}
```   

- C# 코드 구현   

```cs
public int[] InsertionSort(int[] arr)
{

}
```   

________________________________________________________________

## 고급 정렬 알고리즘
> <b><span style="color:black">- 평균 소요 시간이 $$\Theta(n\log n)$$인 정렬 알고리즘</span></b>   
> <b><span style="color:black">- 재귀적 요소가 사용된다</span></b>   
   
### 1. Merge Sort(병합 정렬)   
> <b><span style="color:black">입력을 반으로 나누어 각각 정렬 후 병합하는 형태의 정렬</span></b>   
   
- Pseudo Code   

```
MergeSort(A[], p, r)  //A[p...r]을 정렬
{
  if(p < r) then
  {
    q <- (p + r) / 2;
    MergeSort(A, p, q);
    MergeSort(q + 1, r);
    Merge(A, p, q, r);
  }
}

Merge(A[], p, q, r)
{
  i <- p; j <- q + 1; t <- 1;
  while(i <= q and j <= r)
  {
    if(A[i] <= A[j])
    then tmp[t++] <- A[i++];
    else tmp[t++] <- A[j++];
  }

  while(i <= q)
    tmp[t++] <- A[i++];
  while(j <= r)
    tmp[t++] <- A[j++];
  i <- p; t <- 1;
  while( i <= r)
    A[i++] <- tmp[t++];
}
```   

- C# 코드 구현   

```cs
public int[] MergeSort(int[] arr, int p, int r)
{

}

public int[] Merge(int[] arr, int p, int q, int r)
{

}
```   


### 2. Quick Sort(퀵 정렬)   
> <b><span style="color:black">- 최악의 경우 $$\Theta(n^2)$$의 속도를 가지지만, 평균적으로 가장 높은 성능을 가짐</span></b>   
> <b><span style="color:black">- 기준 원소를 잡고 해당 원소보다 작거나 같으면 왼쪽, 크면 오른쪽으로 배치하는 정렬</span></b>   
   
- Pseudo Code   
   
```
QuickSort(A[], p, r)
{
  if(p < r) then
  {
    q <- Partition(A, p, r);
    QuickSort(A, p, q - 1);
    QuickSort(A, q + 1, r);
  }
}

Partition(A[], p, r)
{
  x <- A[r];
  i <- p - 1;
  for j <- p to r -1
    if(A[j] <= x) then A[++i] <-> A[j];

  A[i + 1] <-> A[r];
  return i + 1;
}
```   

- C# 코드 구현   
   
```cs
public int[] QuickSort(int[] arr, int p, int r)
{
  
}

public int Partition(int[] arr, int p, int r)
{

}
```   
   

### 3. Heap Sort(힙 정렬)   
> <b><span style="color:black">- 힙(이진트리)이라는 특수한 자료구조를 사용하는 정렬</span></b>   
> <b><span style="color:black">- 배열을 힙으로 만들어 주고, A[k]의 자식은 A[2k], A[2k + 1]인 부분을 활용하여 정렬한다. </span></b>   
   
- Pseudo Code   

```
HeapSort(A[], n)
{
  BuildHeap(A, n);
  for i <- n downto 2
  {
    A[1] <-> A[i];
    Heapify(A, 1, i - 1);
  }
}

BuildHeap(A[], n)
{
  for i <- n/2 downto 1
    Heapify(A, i, n);
}

Heapify(A[], k, n)
{
  left <- 2k; right <- 2k + 1;
  if(right <= n) then
  {
    if(A[left] < A[right])
      then smaller <- left;
      else smaller <- right;
  }
  else if(left <= n) then smaller <- left;
  else return;

  if(A[smaller] < A[k]) then
  {
    A[k] <-> A[smaller];
    Heapify(A, smaller, n);
  }
}
```   

- C# 코드 구현   
   
```cs
public int[] HeapSort(int[] arr, int n)
{
  
}

public int[] BuildHeap(int[] arr, int n)
{

}

public void Heapify(int[] arr, int k, int n)
{

}

```   
   
________________________________________________________________

## 특수 정렬 알고리즘
> <b><span style="color:black">입력 원소들이 특수한 성질을 만족하는 경우 소요 시간이 $$\Theta(n\log n)$$보다 빨라지는 정렬 알고리즘</span></b>   

### 1. Radix Sort(기수 정렬)
> <b><span style="color:black">- 입력이 모두 k 자릿수 이하의 자연수인 특수한 경우에만 $$\Theta(n)$$ 시간이 소요되는 정렬</span></b>   
> <b><span style="color:black">- 뒷자리부터 자릿수 별로 정렬한다.</span></b>   
   
- Pseudo Code   
   
```
RadixSort(A[], n, k)
{
  for i <- 1 to k
    //i번째 자릿수에 대해 정렬한다. [O(n) 시간에 끝내야함]
}
```   

- C# 코드 구현   
   
```cs

```   
   
### 2. Counting Sort(계수 정렬)
> <b><span style="color:black">정렬하고자 하는 원소들의 값이 k를 넘지 않는 경우 1부터 k까지의 자연수가 각각 몇번 나타나는지를 세어 원소의 위치를 계산하는 정렬</span></b>   
   
- Pseudo Code   
   
```
CountingSort(A[], B[], n)
{
  for i <- 1 to k
    C[i] < - 0;
  for j <- 1 to n
    C[A[j]]++;
  for i <- 2 to k
     C[i] <- C[i] + C[i - 1];
  for j< - n downto 1
  {
    B[C[A[j]]] <- A[j];
    C[A[j]]--;
  }

}
```   

- C# 코드 구현   
   
```cs

```   
   
