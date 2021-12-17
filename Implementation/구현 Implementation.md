# 구현 (Implementation)

1. 완전탐색 : 모든 경우의 수를 주저 없이 다 계산하는 유형

2. 시뮬레이션 : 문제에서 제시한 알고리즘을 한 단계씩 차례대로 직접 수행해야 하는 유형

`방향을 설정해서 이동하는 문제 : dx, dy라는 별도의 리스트를 만들어 방향을 정하자`



#### 예제 1. 상하좌우

- Python 답안1 `내 코드`

```python
n = int(input())
data = map(str, input().split())

start=[1,1]
for d in data:
    if d == 'U':
        if start[0] - 1 < 1:
            pass
        else:
            start[0] -= 1
    elif d == 'D':
        if start [0] + 1 > n:
            pass
        else:
            start[0] += 1
    elif d == 'L':
        if start[1] - 1 < 1:
            pass
        else:
            start[1] -= 1
    elif d == 'R':
        if start[1] + 1 > n:
            pass
        else:
            start[1] += 1

print(*start)
```

 

- Python 답안2 `dx dy로 이동방향을 기록`

```python
n = int(input())
x,y=1,1
plans = input().split()

dx = [0,0,-1,1]
dy = [-1,1,0,0]
move_types = ['L','R','U','D']

for plan in plans:
    for i in range(len(move_types)):
        if plan == move_types[i]:
            nx = x + dx[i]
            ny = y + dy[i]

    if nx < 1 or ny < 1 or nx > n or ny > n:
        continue
    
    x, y = nx, ny

print(x,y)
```



#### 예제 2. 시각 

- Python 답안1 `완전탐색`

```Python
hour = int(input())
cnt = 0


for i in range(0,hour+1):
    for j in range(60):
        for k in range(60):
            if '3' in str(i)+str(j)+str(k):
                cnt +=1
print(cnt)
```



#### 예제 3. 왕실의 나이트

- Python 답안1

```python
position = input()
x = ord(position[0])
y = int(position[1])
cnt = 0

if y-2 > 0 and x-1 > 96:
    cnt += 1
if y-2 > 0 and x+1 < 105:
    cnt += 1

if y+2 < 9 and x-1 > 96:
    cnt += 1
if y+2 <9 and x+1 <105:
    cnt +=1

if x-2 >96 and y-1 >0:
    cnt +=1
if x-2>96 and y+1<9:
    cnt +=1

if x+2<105 and y-1>0:
    cnt +=1
if x+2 <105 and y+1<9:
    cnt+=1

print(cnt)
```

- Python 답안2 `이동방향을 기록하자`

```python
position = input()
row = int(position[1])
column = int(ord(position[0]))-int(ord('a')) + 1
steps = [(-2,-1), (-1,-2), (1,-2), (2,-1), (2,1), (1,2), (-1,2), (-2,1)]

result = 0
for step in steps:
    next_row = row+step[0]
    next_column = column+step[1]
    
    if next_row >= 1 and next_row <= 8 and next_column >= 1 and next_column <= 8:
        result += 1

print(result)
```



#### 예제 4. 게임 개발

- Python 답안

```python
n, m = map(int, input().split())
d = [[0]*m for _ in range(n)]
x,y,direction = map(int, input().split())
d[x][y] = 1

array = []
for i in range(n):
    array.append(list(map(int, input().split())))

dx = [-1, 0, 1, 0]
dy = [0,1,0,-1]

def turn_left():
    global direction
    direction -= 1
    if direction == -1:
        direction = 3

count=1
turn_time = 0
while True:
    turn_left()
    nx = x+dx[direction]
    ny = y+dy[direction]

    if d[nx][ny] == 0 and array[nx][ny]==0:
        d[nx][ny] =1
        x = nx
        y = ny
        count +=1
        turn_time = 0
        continue

    else:
        turn_time += 1

    if turn_time == 4:
        nx = x-dx[direction]
        ny = y-dy[direction]
        if array[nx][ny] == 0:
            x = nx
            y = ny
        else:
            break

        turn_time = 0

print(count)
```

