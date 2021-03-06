---
layout : post
title : 최단 경로 탐색
subtitle : 특정 지점까지 가장 빠르게 도달하는 방법을 찾는 알고리즘
tags : [Problem Solving]
author : Heeseok Jeong
comments : True
use_math: True
sitemap :
  changefreq : daily
  priority : 1.0
---

# 목차
<br>

- [특징](#특징)
- [다익스트라 최단 경로 알고리즘](#다익스트라-최단-경로-알고리즘)
- [플로이드 워셜 알고리즘](#플로이드-워셜-알고리즘)

<br>
<hr>
<br>

# 특징
<br>

- a.k.a. 길찾기 문제
- 상황에 맞는 효율적인 알고리즘이 정립돼 있음
- 유형
    - 한 지점 → 특정 지점까지 최단 경로 구하기
    - 모든 지점 → 다른 모든 지점까지 최단 경로 구하기 등
- 그래프로 표현

<br>
<hr>
<br>

# 다익스트라 최단 경로 알고리즘
<br>

- 한 지점에서 출발해 다른 노드로 가는 각각의 최단 경로를 구함
- 음의 간선, 0 보다 작은 값을 가지는 간선이 없어야 함!
- 현실 세계의 길은 음의 간선이 없으므로 GPS 소프트웨어에서 활용됨
- 그리디 알고리즘으로 분류됨, 매번 가장 비용이 적은 노드 선택하기 때문
- 입력이 많기 때문에 sys.stdin.readline 사용
- 과정
    1. 출발 노드 설정
    2. 최단 거리 테이블 (1 차원 리스트) 초기화
        - 출발 노드에서 출발 노드는 0
        - 출발 노드에서 다른 노드는 무한으로 초기화 → int(1e9)
    3. 방문하지 않은 노드 중, 최단 거리가 가장 짧은 노트 선택
        - 방문한 곳은 visited 표시
        - 거리가 같을 때는 더 작은 숫자 선택
    4. 해당 노드를 거쳐 다른 노드로 가는 최단 거리 비용을 테이블에 갱신
    5. 3, 4 과정 반복

    ⇒ 최단 경로 테이블이 의미하는 것 : 출발 노드부터 해당 노드까지 소모되는 최소 비용

- 구현 방법
    1. 구현은 쉽지만 느림 (간단한 구현 방법)
    2. 구현 조금 까다롭지만 빠름, 2번 써야함, 정확히 이해하고 구현할 수 있을 때까지 연습하도록! (개선된 다익스트라 알고리즘)
- 한 번 방문한 곳은 더이상 갱신되지 않음 → 한 번의 방문은 한 노드에 대한 최단 거리 보장

### 1. 간단한 구현 방법

- O(V^2) → 노드 개수가 10,000 넘어가면 사용 불가
- 초기에 다익스트라가 고안했던 방법 (원래는 최단 경로를 구하므로 경로에 대한 정보를 다 담아야하지만, 책에서는 코테용으로 최단 거리 정보만 담는 코드 제공)
- 과정
    - 각 노드에 대한 최단 거리를 담는 1차원 리스트 선언
    - 단계마다 방문하지 않은 노드 중, 최단 거리가 가장 짧은 노드를 선택하기 위해 1차원 리스트의 모든 원소를 확인

### 2. 개선된 다익스트라 알고리즘

- O(ElogV)

    : 모든 엣지를 우선순위 큐에 넣었다가 빼내는 과정과 유사 
    → O(ElogE) 
    → O(ElogV^2) (*E < V^2 이므로) 
    → O(2ElogV)

    → O(ElogV)

- 매번 테이블을 보며 최단 거리가 가장 짧은 노드를 찾던 방법에서 힙 자료구조를 사용하여 최단거리에 대한 정보를 얻어냄
- 힙이란?
    - priority queue 를 구현하기 위해 사용하는 자료구조
    → 우선순위가 가장 높은 데이터를 가장 먼저 꺼냄
    - 우선순위 큐를 사용하기 위해 파이썬에서 `PriorityQueue` 나 `heapq` 모듈을 사용할 수 있음, `heapq` 가 더 빨라서 많이 사용
        - 파이썬에서는 기본적으로 최소 힙 사용 (C++ 은 최대 힙, 자바는 최소 힙)
        - 다익스트라 알고리즘에서는 최소 힙 적합
        - 주로 정수를 다룸
        - 만약 최대힙을 사용하고 싶다면, 넣을 때와 뺄 때 값에 - 를 붙이면 된다.
    - 다른 노드까지 소요되는 거리에 대한 정보를 (거리, 노드) 튜플로 힙에 넣는다. (거리가 먼저 나와야 거리순으로 꺼내주기 때문)

    ```python
    import heapq
    import sys
    input = sys.stdin.readline
    INF = int(1e9)

    # 노드 개수, 간선 개수 입력받기
    n, m = map(int, input().split())
    # 시작 노드 번호 입력받기
    start = int(input())
    # 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트 만들기
    graph = [[] for i in range(n+1)]
    # 최단 거리 테이블을 모두 무한으로 초기화
    distance = [INF] * (n+1)

    # 모든 간선 정보 입력받기
    for _ in range(m):
    	a, b, c = map(int, input().split())
    	# a 번 노드에서 b 번 노드로 가는 비용이 c 라는 의미
    	graph[a].append((b, c))

    def dijkstra(start):
    	q = []
    	# 시작 노드로 가기 위한 최단 경로는 0 으로 설정하여, 큐에 삽입
    	heapq.heappush(q, (0, start))
    	distance[start] = 0
    	while q: # 큐가 비어있지 않다면
    		# 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
    		dist, now = heapq.heappop(q)
    		# 현재 노드가 이미 처리된 적이 있는 노드면 무시
    		if distance < dist:
    			continue
    		# 현재 노드와 연결된 다른 인접한 노드들을 확인
    		for to_other in graph[now]:
    			cost = dist + to_other[1]
    			if distance[to_other[0]] > cost:
    				distance[to_other[0]] = cost
    				heapq.heappush(q, (cost, to_other[0]))

    # 다익스트라 알고리즘 수행
    dijkstra(start)

    # 모든 노드로 가기 위한 최단 거리를 출력
    for i in range(1, n+1):
    	# 도달할 수 없는 경우, 무한으로 출력
    	if distance[i] == INF:
    		print("INFINITY")
    	else:
    		print(distance[i])
    ```
<br>
<hr>
<br>

# 플로이드 워셜 알고리즘
<br>

- 다익스트라 알고리즘이 한 지점 → 모든 지점 최단 경로 구하는 알고리즘이었다면, 플로이드 워셜 알고리즘은 모든 지점에서 모든 지점의 최단 경로를 구하는 알고리즘!
- N 개의 단계를 거치면서 단계마다 현재 노드를 거쳐가는 모든 경로에 대한 연산 N^2 을 수행
- 2 차원 리스트에 모든 경로에 대한 최단 경로 저장 (N^2 수행 원인)
- 다익스트라는 그리디였다면, 플로이드 워셜은 DP (점화식에 맞게 2 차원 리스트 수정)
- 현재 확인하고 있는 노드 (X) 제외하고 나머지 노드 중에서 두 노드 (A, B) 를 쌍으로 둔다 (A → X → B 경로 거리 탐색) .
- 즉, A → B 최단 경로의 값을 A → X → B 의 값과 비교하여 갱신한다.
- 각 단계에 대한 점화식
    - $D_\mathit{ab} = min(D_\mathit{ab},\ D_\mathit{ak}\ +\ D_\mathit{kb})$

```python
INF = int(1e9) # 무한을 의미하는 값으로 10 억을 설정

# 노드의 개수 및 간선의 개수를 입력받기
n = int(input())
m = int(input())
# 2 차원 리스트 (그래프 표현) 를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n+1) for _ in range(n+1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0 으로 초기화
for i in range(1, n+1):
	graph[i][i] = 0

# 각 간선에 대한 정보를 입력받아, 그 값으로 초기화
for _ in range(m):
	# A 에서 B 로 가는 비용은 C 라고 설정
	a, b, c = map(int, input().split())
	graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n+1):
	for a in range(1, n+1):
		for b in range(1, n+1):
			graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b]

# 수행된 결과를 출력
for a in range(1, n+1):
	for b in range(1, n+1):
		# 도달할 수 없는 경우, 무한으로 출력
		if graph[a][b] == INF:
			print("INFINITY")
		else:
			print(graph[a][b], end = ' ')
	print()

```

<br>

<br>

⇒ 플로이드 워셜은 간단해서 비슷하게 구현 잘 했지만, 다익스트라는 많이 다르게 생각해서 다익스트라 문제 더 풀면서 이 스타일 익혀야 함

<br>
<hr>
<br>

# 참조
<br>

- part2, 이것이 취업을 위한 코딩테스트다 with 파이썬
