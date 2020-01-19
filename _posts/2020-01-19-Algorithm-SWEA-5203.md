---
title: "[파이썬 S/W 문제해결 구현] SWEA 5203 - 베이비진 게임"
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
- SWEA 5203 - [파이썬 S/W 문제해결 구현 3일차] - 베이비진 게임
- [문제 링크](https://swexpertacademy.com/main/learn/course/subjectDetail.do?courseId=AVuPDYSqAAbw5UW6&subjectId=AWUYEGw61n8DFAVT#)
- 문제의 저작권은 SW Expert Academy에 있으며 무단 복사/배포를 금지 합니다.
  
  
# Solution
이 문제의 핵심은 triplet과 run을 어떻게 판별하느냐인데 내가 해결한 방법은 다음과 같다.  
- tiplet인 경우
	+ 숫자의 개수를 count한 배열에 3이 있는지 확인
- run인 경우
	+ 숫자의 개수를 count한 배열 중 0이상인 값의 인덱스를 뽑아 한 칸 떨어진 인덱스의 차이가 2인지 확인(3개의 숫자가 연속이 되려면 인덱스의 차이가 2일 수 밖에 없다.)  

```python
def Is_triplet(numbers):
    return True if 3 in numbers else False

def Is_run(numbers):
    card = [i for i in range(len(numbers)) if numbers[i] > 0]
    for i in range(2,len(card)):
        if card[i] - card[i-2] == 2:
            return True
    return False

def who_Is_Winner(first, second):
    # 플레이어1이 이기는 경우
    if (Is_triplet(first) or Is_run(first)) and (not (Is_triplet(second)) and not (Is_run(second))):
        return 1
    # 플레이어2가 이기는 경우
    elif (Is_triplet(second) or Is_run(second)) and (not (Is_triplet(first)) and not (Is_run(first))):
        return 2
    else:
        return 0


T = int(input())
# 여러개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
for test_case in range(1, T + 1):
    number = list(map(int, input().split()))
    first = [0]*10
    second = [0]*10
    winner = 0
    for i in range(len(number)):
        if i > 5:
            winner = who_Is_Winner(first, second)
            if winner > 0:
                break
        if i % 2:
            second[number[i]] += 1
        else:
            first[number[i]] += 1
    winner = who_Is_Winner(first, second)
    print('#%d'%test_case, winner)
```

