# 그리디 greedy

- 현재 상황에서 지금 당장 좋은 것만 고르는 방법

- 문제 해결 아이디어만 떠올린다면 풀 수 있는 알고리즘



### 예제1. 거스름돈

당신은 음식점의 계산을 도와주는 점원이다. 카운터에는 거스름돈으로 사용할 500원, 100원, 50원, 10원짜리 동전이 무한히 존재한다고 가정한다. 손님에게 거슬러 줘야 할 돈이 N원일 때 거슬러 줘야 할 동전의 최소 개수를 구하라. 단, 거슬러 줘야 할 돈 N은 항상 10의 배수이다.

- 문제 해설

  - 문제 해결 방법 : 가장 큰 화폐 단위부터 돈을 거슬러 주는 것

- Python 답안

  - ```python
    n = 1260
    count = 0
    # 큰 단위의 화폐부터 차례대로 확인
    coin_types = [500, 100, 50, 10]
    
    for coin in coin_types:
        count += n//coin
        n %= coin
    print(count)
    ```

  - 알고리즘의 시간 복잡도는 동전의 총 종류에만 영향을 받고, 거슬러 줘야 하는 금액의 크기와는 무관하다는 것을 알 수 있다.



### 예제2. 큰 수의 법칙

- 문제 해설

  - 문제 해결 방법 : `반복되는 수열을 파악`

    

- Python 답안1 `수가 커지면 시간초과 오류 발생` 

```PYTHON
n,m,k = map(int,input().split())
arr = list(map(int,input().split()))
arr.sort()
answer = 0
first = arr[-1]
second = arr[-2]

while True:
    for _ in range(k):
        if m == 0:
            break
        answer += first
        m-=1
    if m==0:
        break
    answer+=second
    m-=1
print(answer)
```

- Python 답안2  

```python
N,M,K = map(int,input().split())
data = list(map(int, input().split()))
data.sort()
first = M//(K+1)*K + M%(K+1)
second = M//(K+1)

answer = first*data[-1]+second*data[-2]
print(answer)
```



### 예시3. 숫자 카드 게임

- 문제 해설
  - 문제 해결 방법 : `각 행마다 가장 작은 수를 찾은 뒤에 그 수 중에서 가장 큰 수를 찾기`

- Python 답안1

```python
n, m = map(int, input().split())
data = [map(int, input().split()) for _ in range(n)]
li=[]
for i in data:
    li.append(min(i))
print(max(li))
```

- Python 답안2

```python
n, m = map(int, input().split())
result = 0
for i in range(n):
    data = list(map(int, input().split()))
    min_value = min(data)
    result = max(result, min_value)
print(result)
```



### 예시4. 1이 될 때까지

- 문제 해설
  - 문제 해결 방법 : `최대한 많이 나누기`

- Python 답안1 `시간 초과 오류`

```python
n,k = map(int, input().split())
cnt = 0
while n != 1:
    if n%k == 0:
        n /= k
        cnt += 1
    else:
        n -= 1
        cnt += 1
print(cnt)
```



- Python 답안2

```python
n,k = map(int, input().split())
cnt = 0

while True:
    target = n//k * k
    cnt += (n-target)
    n = target
    if n<k:
        break
    n //= k
    cnt += 1

cnt += n-1
print(cnt)
```

