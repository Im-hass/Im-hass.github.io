---
layout: default
title: Algorithms
# nav_order: 3
has_children: true
permalink: /docs/algorithms
---

# Algorithms


## 공간 복잡도(Space Complexity)
- 프로그램을 실행시킨 후 완료하는 데 필요로 하는 **자원 공간의 양.**

## 시간 복잡도(Time Complexity)
- 알고리즘을 수행하는 데 **연산들이 몇 번 이루어지는 지**를 숫자로 표기한 것.
- 연산의 종류는 산술, 대입, 비교, 이동 등을 말한다.
- 시간과 공간은 반비례적인 경향이 있기 때문에 알고리즘의 척도는 시간 복잡도를 위주로 판단한다.

## 표기법
### Big O 표기법(Big-Oh Notation)
- 컴퓨터 과학에서 “대략”을 나타내는 공식적인 개념.
- **최악의 경우(실행 시간의 상한 = 제일 느린 경우)에 대한 복잡도**를 나타내는 표현이다.

| 표기 | 예시 |
|:---|:---|
| O(1) | - |
| O(log n) | binary search(이진 탐색) |
| O(n) | linear search(선형 탐색) |
| O(n log n) | quick sort(퀵 정렬) |
| O(n^2) | bubble sort(거품 정렬)<br/>insertion sort(삽입 정렬)<br/>selection sort(선택 정렬) |
| O(n^3) | - |
| O(2^n) | - |
| O(n^k) | - |

### Big Ω 표기법(Big-Omega Notation)
- Big-O와 반대되는 개념으로 **최선의 경우(실행 시간의 하한 = 제일 빠른 경우)에 대한 복잡도**를 나타내는 표현이다.

| 표기 | 예시 |
|:---|:---|
| Ω(1) | linear search(선형 탐색)<br/>binary search(이진 탐색)|
| Ω(log n) | - |
| Ω(n) | bubble sort(거품 정렬)<br/>insertion sort(삽입 정렬) |
| Ω(n log n) | - |
| Ω(n^2) | selection sort(선택 정렬) |

### Big θ 표기법(Big-Theta Notation)
- **평균 실행 시간에 대한 복잡도**를 나타내는 표현이다.

## 참고
- [시간 복잡도, 공간 복잡도](https://madplay.github.io/post/time-complexity-space-complexity)
- [CS50 - 알고리즘 표기법](https://www.boostcourse.org/cs112/lecture/119020?isDesc=false)
