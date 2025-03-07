---
layout: post
title: Algorithm - DFS[Depth-First Serch]
author: Hyunwoo Soung
categories: study
tags:
  - Sort
  - Algorithm
image: algorithm.jpg
published: true
---
[내용 참조 : https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html](https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html)   
이해 후 정리 필요   

## DFS[깊이 우선 탐색]   
   
### 1. 깊이 우선 탐색이란  
#### 루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기(branch)로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법  

- 미로를 탐색할 때 한 방향으로 갈 수 있을 때까지 계속 가다가 더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길로 돌아와서 이곳으로부터 다른 방향으로 다시 탐색을 진행하는 방법과 유사하다.  
- 즉, 넓게(wide) 탐색하기 전에 깊게(deep) 탐색하는 것이다.  
- 사용하는 경우: 모든 노드를 방문 하고자 하는 경우에 이 방법을 선택한다.  
- 깊이 우선 탐색(DFS)이 너비 우선 탐색(BFS)보다 좀 더 간단하다.  
- 단순 검색 속도 자체는 너비 우선 탐색(BFS)에 비해서 느리다.  
<br><br>

### 2. 깊이 우선 탐색(DFS)의 특징
- 자기 자신을 호출하는 순환 알고리즘의 형태 를 가지고 있다.   
- 전위 순회(Pre-Order Traversals)를 포함한 다른 형태의 트리 순회는 모두 DFS의 한 종류이다.   
- 이 알고리즘을 구현할 때 가장 큰 차이점은, 그래프 탐색의 경우 어떤 노드를 방문했었는지 여부를 반드시 검사 해야 한다는 것이다.   
- 이를 검사하지 않을 경우 무한루프에 빠질 위험이 있다.   
<br><br>

+ Pseudo code   

 ```
void search(Node root) {
  if (root == null) return;
  // 1. root 노드 방문
  visit(root);
  root.visited = true; // 1-1. 방문한 노드를 표시
  // 2. root 노드와 인접한 정점을 모두 방문
  for each (Node n in root.adjacent) {
    if (n.visited == false) { // 4. 방문하지 않은 정점을 찾는다.
      search(n); // 3. root 노드와 인접한 정점 정점을 시작 정점으로 DFS를 시작
    }
  }
}

 ```

### 3. 깊이 우선 탐색(DFS)의 시간 복잡도  
   
- DFS는 그래프(정점의 수: N, 간선의 수: E)의 모든 간선을 조회한다.  
- 인접 리스트로 표현된 그래프: O(N+E)  
- 인접 행렬로 표현된 그래프: O(N^2)  
- 즉, 그래프 내에 적은 숫자의 간선만을 가지는 희소 그래프(Sparse Graph) 의 경우 인접 행렬보다 인접 리스트를 사용하는 것이 유리하다.  