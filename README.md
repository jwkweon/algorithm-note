# 코테 대비 노트 

## 정렬
sort(), sorted() 에서 key를 이용한 정렬

첫번째 인자 기준 오름차순으로 정렬

ex: `arr = sorted(arr, key= lambda x : x[0])`

두번째 인자 기준 오름차순 다음 첫번째 인자 기준 오름차순 정렬

ex: `arr = sorted(arr, key= lambda x : (x[1], x[0]))`

딕셔너리 값으로 정렬 : 두번째 인자 역순

ex:
```py
sorted_dict = sorted(my_dict.items(), key = lambda item: -item[1])
print(sorted_dict)
```

`reverse = True` 도 가능
    
```py
sorted_dict = sorted(my_dict.items(), key = lambda item: item[1], reverse=True)
print(sorted_dict)
```

## Dijkstra

우선순위 큐로 구현
전반적인 코드 동작 원리 이해

```py
import heapq

'''
distance, graph 처리
'''

def dijkstra(start):
    # 초기조건
    q = []
    heapq.heappush(q, (0, start))
    distance[start] = 0
    
    while q:
        dist, n = heapq.heappop(q)
        
        if distance[now] < dist:
            continue
        
        for i in graph[now]:
            cost = dist + i[1] # value
            if cost < distance[i[0]]:
                # update
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

```



## heapq

```py
hq = []
# 최소힙
for ...
    heapq.heappush(hq, val)

# 최대힙
for ...
    heapq.heappush(hq, -val)
    
# 리스트 -> 힙
heapq.heapify(list)
```

### 단순한 tip

- 리스트에 n개 원소 
```py
[False] * n
[0] * n
```

- 문자열 내 특수 기호 제거

정규 표현식 `re.sub`을 이용해서 제거
```py
import re

str_input = '...'

out = re.sub('[^A-Za-z0-9가-힣]', '', str_input)

```

### itertools

- product

### 가장 긴 증가하는 수열 & 가장 긴 감소하는 수열 & 혼합

```py
n = int(input())
arr = list(map(int, input().split()))
rv_arr = arr[::-1]  # 감소 수열 찾기위해
lis = [1] * n
lds = [1] * n

for i in range(n):
    for j in range(i):
        if arr[i] > arr[j]:
            lis[i] = max(lis[i], lis[j] + 1)    # 가장 긴 증가수열
        
        if rv_arr[i] > rv_arr[j]:
            lds[i] = max(lds[i], lds[j] + 1)     # 가장 긴 감소수열

ans = [x+y for x,y in zip(lis, lds[::-1])]

print(max(ans)-1) # 증가했다가 감소하는 수열 중 제일 긴 것       

```
