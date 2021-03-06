---
layout : post
title : DFS/BFS
subtitle : 그래프를 탐색하기 위한 대표적인 두 알고리즘
tags : [Problem Solving]
author : Heeseok Jeong
comments : True
sitemap :
  changefreq : daily
  priority : 1.0
---

### 탐색

- 많은 양의 데이터 중, 원하는 데이터를 찾는 과정
- 그래프, 트리 등의 자료구조 안에서 탐색이 주를 이룸
- DFS 와 BFS 에서는 **인접 행렬**(2차원 배열로 그래프의 연결 관계를 표현) 과 **인접 리스트**(리스트로 그래프의 연결 관계를 표현) 로 표현
- 인접 행렬
    - 2차원 리스트 사용
    - 메모리 많이 씀, 정보를 얻는 데에는 빠름
- 인접 리스트
    - map 으로 키 값을 시작 노드, 밸류에 도착 노드와 거리 등을 저장 할 수 있음
    - 튜플을 저장하는 2차원 리스트로 해당 행 → (노드, 거리) 형태도 가능
    - 메모리 효율적으로 씀, 하지만 연결된 데이터를 하나씩 확인하므로 특정한 두 노드가 연결되어 있는지에 대한 정보를 얻는 데에는 느림

<br>
### DFS

- 스택 사용
    - FILO (선입후출 or 후입선출) 구조
    - 파이썬에서는 기본 리스트의 append() 와 pop() 함수 사용하면 됨
- 재귀 함수
    - 자기 자신을 다시 호출하는 함수
    - 최대 재귀 깊이 초과 조심해야 함
    - 컴퓨터 내부에서는 재귀 함수를 스택으로 처리함
    - 종료 조건이 중요
        - 종료 조건이 없으면 무한 호출!
    - 반복문 대신 사용할 수 있는데, 코드가 더 간결해짐, 수학의 점화식을 그대로 소스코드로 옮기기 때문
- 깊이 우선 탐색
- 동작
    1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
    2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 있으면 그 인접 노드를 스택에 넣고 방문 처리를 한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
    3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.
- 동빈북은 실제 스택 사용은 없고 재귀 함수만 사용 (간결하기 때문)

<br>
### BFS

- 큐 사용
    - FIFO (선입선출) 구조
    - 파이썬에서는 collections 모듈의 `deque` 사용
        - appendleft() 와 popleft() 함수 사용
        - deque 객체를 리스트로 변경하려면 list(deq) 하면 됨
    - 너비 우선 탐색
    - 동작
        1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
        2. 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리를 한다.
        3. 2번의 과정을 더 이상 수행할 수 없을 때까지 반복한다.
    - 일반적으로 재귀 DFS 보다 수행 시간이 빠름

<br>
### 실전문제

NxM 미로가 주어졌을 때 0, 0 지점에서 n, m 지점으로 가는 최단 거리 구하기

- 나는 dfs로 몇 칸 갔는지 count라는 전역변수를 체크하는 방법을 사용했지만,  솔루션은 bfs로 직접 그래프에 몇 칸 이동했는지를 기록하는 방법을 사용함 (bfs 에서는 처음 방문하는 순간이 최단거리를 보장해줌)

<br>
<hr>
<br>

# 참조
<br>

- part2, 이것이 취업을 위한 코딩테스트다 with 파이썬
