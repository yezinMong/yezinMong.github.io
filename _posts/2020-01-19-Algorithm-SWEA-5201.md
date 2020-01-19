---
title: "[파이썬 S/W 문제해결 구현] SWEA 5201 - 컨테이너 운반"
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
- SWEA 5201 - [파이썬 S/W 문제해결 구현 3일차] - 컨테이너 운반
- [문제 링크](https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYEGw61n8DFAVT#)
- 문제의 저작권은 SW Expert Academy에 있으며 무단 복사/배포를 금지 합니다.
  
  
# Solution
이 문제의 핵심은 컨테이너 무게와 트럭의 적재용량을 내림차순으로 정렬한 뒤 비교하는 것이다.  
```python
T = int(input())
# 여러개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
for test_case in range(1, T + 1):
    N, M = map(int, input().strip().split())
    container = sorted(list(map(int, input().strip().split())), reverse=True)
    truck = sorted(list(map(int, input().strip().split())), reverse=True)

    weight = 0
    i = j = 0
    while True:
        if i == len(container) or j == len(truck):
            break
        if container[i] <= truck[j]:
            weight += container[i]
            j += 1
        i += 1
    print('#%d'%test_case, weight)
```

