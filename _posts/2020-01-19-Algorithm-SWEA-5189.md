---
title: "[파이썬 S/W 문제해결 구현] SWEA 5189 - 전자카트"
excerpt: "SW Expert Academy Programming Advanced - 02 완전 검색"

categories:
  - Algorithm
tags:
  - python
  - SWEA
  - Algorithm
---

# 문제
- SWEA 5189 - [파이썬 S/W 문제해결 구현 2일차] - 전자카트
- [문제 링크](https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYDrI61lYDFAVT)
- 문제의 저작권은 SW Expert Academy에 있으며 무단 복사/배포를 금지 합니다.

# Solution
이 문제의 핵심은 2번부터 N번까지의 순열을 구하는 것이다.  
N의 범위가 3<=N<=10이므로 python의 permutation 라이브러리를 사용하면 쉽게 구할 수 있다.  

```python
from itertools import permutations

T = int(input())
# 여러개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
for test_case in range(1, T + 1):
    N = int(input())
    region = [list(map(int, input().strip().split())) for _ in range(N)]
    temp = [i for i in range(1, N)]
    myperms = list(permutations(temp, N-1))

    minimum = 999999
    for perm in myperms:
        using = region[0][perm[0]]
        for i in range(len(perm)-1):
            using += region[perm[i]][perm[i+1]]
        using += region[perm[-1]][0]
        if minimum > using:
            minimum = using
    print('#%d'%test_case, minimum)

```
