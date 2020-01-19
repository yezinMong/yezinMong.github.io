---
title: "[파이썬 S/W 문제해결 구현] SWEA 5202 - 화물 도크"
excerpt: "SW Expert Academy Programming Advanced - 03 탐욕 알고리즘"

categories:
  - Algorithm
tags:
  - python
  - SWEA
  - Algorithm
  - greedy
---

# 문제
- SWEA 5202 - [파이썬 S/W 문제해결 구현 3일차] - 화물 도크
- [문제 링크](https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYEGw61n8DFAVT#)
- 문제의 저작권은 SW Expert Academy에 있으며 무단 복사/배포를 금지 합니다.
  
  
# Solution
이 문제는 겹치지 않는 작업 시간 내에 가장 많은 화물차의 대수를 구하는 전형적인 활동 선택 문제로 그리디 알고리즘으로 풀 수 있다.  
처음엔 그리디말고 시간 배열에 1씩 더해 작업을 하고 있는지 안 하고 있는지를 표시하는 방법으로 풀려다가 끝나는 시간과 시작 시간이 겹치는 부분을 해결하지 못했다.  


> 그리디 알고리즘을 사용한 해결 방법
1. 끝나는 시간이 빠른 순서로 작업 시간 정렬
2. 첫 번째로 끝나는 작업을 해집합에 포함
3. 선택한 작업 종료 시간보다 빠른 시작 시간을 가지는 작업은 pass  


```python
T = int(input())
# 여러개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
for test_case in range(1, T + 1):
    N = int(input())
    work = []
    for _ in range(N):
        s,e = map(int, input().split())
        work.append((s,e))

    work = sorted(work, key=lambda x:(x[1])) # 종료시간이 빠른 순으로 정렬
    time = 0
    cnt = 0
    for start, end in work:
        if start >= time: # 종료 시간이 시작 시간 이하이면
            time = end
            cnt += 1
    print('#%d'%test_case, cnt)
```
