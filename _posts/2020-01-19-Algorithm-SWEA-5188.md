---
title: "[파이썬 S/W 문제해결 구현] SWEA 5188 - 최소합"
excerpt: "SW Expert Academy Programming Advanced - 02 완전 검색"

categories:
  - Algorithm
tags:
  - python
  - SWEA
  - Algorithm
---

# 문제
- SWEA 5188 - [파이썬 S/W 문제해결 구현 2일차] - 최소합
- [문제 링크](https://swexpertacademy.com/main/learn/course/lectureProblemViewer.do)
- 문제의 저작권은 SW Expert Academy에 있으며 무단 복사/배포를 금지 합니다.

# 나의 풀이
문제는 가능한 모든 경로에 대해 최소합을 구하는 것이다.  
처음엔 오른쪽 방향과 아래쪽 방향을 0, 1로 두어 (N-1)*2개 즉, 만약 N이 3이라면 [0,0,1,1]로 두어 permutation을 만든 다음 set으로 중복을 제거하려 했다. 이렇게 되면 [0,0,1,1],[0,1,0,1],[0,1,1,0],[1,0,0,1],[1,0,1,0,],[1,1,0,0]의 조합이 나오고 각 방향에 위치한 값들을 더하며 최종적으로 최소합을 구하려 했으나 N의 범위가 커질수록 기하급수적으로 시간복잡도가 증가하게 된다.  
  
따라서, DP로 이전 위치의 최소합들을 누적해가며 최종적으로 마지막 도착지엔 최소합이 저장되게 하였다.  
여기서 주의할 점은 row와 col이 각각 0일 때의 예외처리를 해주는 것.  

```python
T = int(input())
# 여러개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
for test_case in range(1, T + 1):
    N = int(input())
    DP = [list(map(int, input().strip().split())) for _ in range(N)]
    minimum = [[0 for _ in range(N)] for _ in range(N)]
    minimum[0][0] = DP[0][0]
    for r in range(N):
        for c in range(N):
            temp = 0
            if r == 0 and c > 0:
                minimum[r][c] = minimum[r][c-1] + DP[r][c]
            elif c == 0 and r > 0:
                minimum[r][c] = minimum[r-1][c] + DP[r][c]
            else:
                if minimum[r-1][c] > minimum[r][c-1]:
                    minimum[r][c] = minimum[r][c-1] + DP[r][c]
                else:
                    minimum[r][c] = minimum[r-1][c] + DP[r][c]
    print('#%d'%test_case, minimum[N-1][N-1])

```
