---
layout : post
title : 아이디어를 코드로 바꾸는 구현
subtitle : Implementation
tags : [Problem Solving]
author : Heeseok Jeong
comments : True
sitemap :
  changefreq : daily
  priority : 1.0
---


## 특징

- 문제를 읽고 방법을 생각하여 문제를 해결할 때, 생각은 했으나 구현하기 어려운 유형
- 피지컬(문법 능숙 + 작성 속도 빠르게) 중요
- 구현하기 어려운 문제
    - 알고리즘은 간단한데 코드가 지나치게 길어지는 문제
    - 특정 소수점 자리까지 출력하는 문제
    - 문자열 입력에서 한 문자 단위로 끊어서 파싱하는 문제 등
    - 사소한 조건이 많은 문제
- 팁 : 라이브러리 활용 잘해야 함
- 완전탐색과 시뮬레이션도 구현에 포함시킴
- 완전탐색 : 모든 경우의 수를 주저 없이 다 계산
- 시뮬레이션 : 문제에서 제시한 알고리즘을 한 단계씩 차례대로 직접 수행
- C++ 에서는 int가 -20억 ~ 20억 처리해서 long long 쓰는 경우도 있는데, 파이썬은 자동이라 편함
- 파이썬 배열 크기 제한
    - 보통 128~512MB 가능
    - 천만 → 40M 이므로 여러개 쓰면 위험함. 따라서 그냥 천만 정도되는 리스트 만들어야 하는 경우엔 다른 생각하자
- 하지만 대회 문제 아닌 이상, 복잡한 최적화 문제는 안 냄. 그냥 통과 목표로 하자.
- *중요 : 파이썬(3.7v)은 1초에 2천만번 수행이라 보면 됨
- 문제 풀 때, 데이터 입력 범위 잘보고 시간복잡도 미리 생각하는게 현명함. 예를 들어 N = 백만이면 NlogN 써야함. NlogN = 2천만 → 1초.


<br>
### 실전문제) 게임 개발

지도 상에 로봇이 움직일 수 있는 구역과 없는 구역 구분되고 더이상 움직일 수 없는 조건 만족하면 멈추고 탐색한 칸 찾는 프로그램.

- dx와 dy를 설정하는 것이 중요
- 이런 유형 삼성 코테에 자주 나옴
- turn_left() 동작만 함수로 뺌, global 변수 사용
- 4방향 확인하는 변수 만들어 씀
- 내 솔루션은 방문한 곳을 2 로 체크한 반면, 동빈북은 따로 로봇이 가는 곳 표시하는 지도를 만듦. 일반적으론 내방법이 더 나아보이나 상황에 맞게 쓰면 될 듯.


<br>
<hr>
<br>

# 참조
<br>

- part2, 이것이 취업을 위한 코딩테스트다 with 파이썬
