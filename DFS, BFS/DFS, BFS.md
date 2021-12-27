# DFS/BFS

- 그래프를 `탐색`하기 위한 대표적인 두 가지 알고리즘으로,  스택과 큐에 대한 이해가 전제되어야함

- 탐색 : `많은 양의 데이터 중에서 원하는 데이터를 찾는 과정`

- 자료구조 : `데이터를 표현하고 관리하고 처리하기 위한 구조, `  기초 개념 : 스택, 큐



## 1. 자료구조 기초



#### 스택(Stack)

- 박스쌓기에 비유, 선입후출(FILO) 구조 혹은 후입선출(LIFO) 구조

```python
stack = []

# 삽입(5) - 삽입(2) - 삽입(3) - 삽입(7) - 삭제() - 삽입(1) - 삽입(4) - 삭제()
stack.append(5)
stack.append(2)
stack.append(3)
stack.append(7)
stack.pop()
stack.append(1)
stack.append(4)
stack.pop()

print(stack) # 최하단 원소부터 출력
print(stack[::-1]) # 최상단 원소부터 출력
```

 

#### 큐(Queue)

- 대기 줄에 비유, 선입선출(FIFO) 구조
- 스택과 큐의 장점을 모두 채택
- 리스트 자료형으로 형변환 : list(deque객체)

```python
from collections import deque

# 큐(Queue) 구현을 위해 deque 라이브러리 사용
queue = deque()

# 삽입(5) - 삽입(2) - 삽입(3) - 삽입(7) - 삭제() - 삽입(1) - 삽입(4) - 삭제()
queue.append(5)
queue.append(2)
queue.append(3)
queue.append(7)
queue.popleft()
queue.append(1)
queue.append(4)
queue.popleft()

print(queue)    # 먼저 들어온 순서대로 출력
queue.reverse() # 다음 출력을 위해 역순으로 바꾸기
print(queue)    # 나중에 들어온 원소부터 출력
```



#### 재귀 함수

- `자기 자신을 다시 호출하는 함수`

  ![](https://t1.daumcdn.net/cfile/tistory/225FB54E5950629713)

- 가장 간단한 재귀 함수

  ```python
  def recursive_function():
  	print('재귀 함수를 호출합니다.')
  	recursive_function()
  
  recursive_function()
  ```

- 재귀 함수의 종료 조건  `종료 조건 꼭 명시해야 함!`

  ```python
  def recursive_function(i):
  	# 100번째 출력했을 때 종료되도록 종료 조건 명시
  	if i == 100:
  		return
  	print(i, '번째 재귀 함수에서', i+1, '번째 지귀 함수를 호출합니다.')
  	recursive_function(i+1)
  	print(i, '번째 재귀 함수를 종료합니다.')
  	
  recursive_function(1)
  ```

  

- n!을 반복적으로 구현 vs 재귀적으로 구현

  ```python
  # 반복적으로 구현한 n!
  def factorial_iterative(n):
      result = 1
      for i in range(1, n+1):
          result *= i
      return result
  
  # 재귀적으로 구현한 n!
  def factorial_recursive(n):
      if n <= 1:
          return 1
      return n * factorial_recursive(n-1)
  
  # 각각의 방식으로 구현한 n! 출력 (n=5)
  print('반복적으로 구현:', factorial_iterative(5))
  print('재귀적으로 구현:', factorial_recursive(5))
  ```



## 2. 탐색 알고리즘 DFS/BFS



#### DFS

- 깊이 우선 탐색이라고 부르며, 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘

1. 인접 행렬 : 2차원 배열로 그래프의 연결 관계를 표현하는 방식

   ![](https://media.vlpt.us/post-images/underlier12/3be338e0-3ab5-11ea-8c7a-6f3522c89aae/image.png)

   

   ```PYTHON
   INF = 99999999 # 무한의 비용 선언
   
   # 2차원 리스트를 이용해 인접 행렬 표현
   graph = [
       [0,7,5],
       [7,0,INF],
       [5,INF,0]
   ]
   
   print(graph)
   ```

   

2. 인접 리스트 : 리스트로 그래프의 연결 관계를 표현하는 방식

   ![](https://t1.daumcdn.net/cfile/tistory/2236CE4D5858CAA032)



​	

```python
# 행(row)이 3개인 2차원 리스트로 인접 리스트 표현
graph = [[] for _ in range(3)]

# 노드 0에 연결된 노드 정보 저장 (노드, 거리)
graph[0].append((1,7))
graph[0].append((2,5))

# 노드 1에 연결된 노드 정보 저장 (노드, 거리)
grpah[1].append((0,7))

# 노드 1에 연결된 노드 정보 저장 (노드, 거리)
graph[2].append((0,5))

print(graph) # [[(1,7),(2,5)], [(0,7)], [(0,5)]]
```



- DFS 예제

  ```PYTHON
  # DFS 메서드 정의
  def dfs(graph, v, visited):
      # 현재 노드를 방문 처리
      visited[v] = True
      print(v, end=' ')
      # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
      for i in graph[v]:
          if not visited[i]:
              dfs(graph, i, visited)
  
  # 각 노드가 연결된 정보를 리스트 자료형으로 표현 (2차원 리스트)
  graph = [
      [],
      [2,3,8],
      [1,7],
      [1,4,5],
      [3,5],
      [3,4],
      [7],
      [2,6,8],
      [1,7]
  ]
  
  # 각 노드가 방문된 정보를 리스트 자료형으로 표현 (1차원 리스트)
  visited = [False] * 9
  
  # 정의된 DFS 함수 호출
  dfs(graph, 1, visited) # 1 2 7 6 8 3 4 5
  ```

  

#### BFS

- 가까운 노드부터 탐색하는 알고리즘, 너비 우선 탐색이라는 의미를 가짐

- 선입선출 방식인 큐 자료구조를 이용해야 함

- DFS보다 구현이 조금 더 빠르게 동작한다

- BFS 예제

  ```PYTHON
  from collections import deque
  
  # BFS 메서드 정의
  def bfs(graph, start, visited):
      # 큐(Queue) 구현을 위해 deque 라이브러리 사용
      queue = deque([start])
      # 현재 노드를 방문 처리
      visitied[start] = True
      # 큐가 빌 때까지 반복
      while queue:
          # 큐에서 하나의 원소를 뽑아 출력
          v = queue.popleft()
          print(v, end = ' ')
          # 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
          for i in graph[v]:
              if not visitied[i]:
                  queue.append(i)
                  visitied[i] = True
                  
  # 각 노드가 연결된 정보를 리스트 자료형으로 표현 (2차원 리스트)
  graph = [
      [],
      [2,3,8],
      [1,7],
      [1,4,5],
      [3,5],
      [3,4],
      [7],
      [2,6,8],
      [1,7]
  ]
  
  # 각 노드가 방문된 정보를 리스트 자료형으로 표현(1차원 리스트)
  visited = [False] * 9
  
  # 정의된 BFS 함수 호출
  bfs(graph, 1, visited) # 1 2 3 8 7 4 5 6
  ```





#### 정리

|           | DFS            | BFS              |
| :-------- | :------------- | :--------------- |
| 동작 원리 | 스택           | 큐               |
| 구현 방법 | 재귀 함수 이용 | 큐 자료구조 이용 |





