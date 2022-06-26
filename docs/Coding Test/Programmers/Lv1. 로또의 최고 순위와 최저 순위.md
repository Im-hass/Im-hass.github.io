---
layout: default
title: Lv1. 로또의 최고 순위와 최저 순위
parent: Programmers
grand_parent: Coding Test
permalink: /docs/coding-test/programmers/Lv1_로또의_최고_순위와_최저 순위
nav_order: 2
---

# Lv1. 로또의 최고 순위와 최저 순위
{: .fw-500 }

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/77484)

Java
{: .label .mt-3 }

Lv1
{: .label .label-purple }

Success
{: .label .label-green }

## 문제 풀이
- 로또 : 1부터 45까지의 숫자 중 6개를 찍어서 맞힌다.
- 알아볼 수 없는 번호가 0으로 표기될 때, 구매한 로또로 당첨이 가능한 최고 순위와 최저 순위를 출력한다.

| 순위   | 당첨 내용            |
|:-|:--------------------|
| 1      | 6개 번호가 모두 일치  |
| 2      | 5개 번호가 일치      |
| 3      | 4개 번호가 일치      |
| 4      | 3개 번호가 일치      |
| 5      | 2개 번호가 일치      |
| 6(낙첨) | 그 외              |

## 주의 사항
- `ArrayList`를 사용하면 배열 내에 값이 포함되는지 `contains()` 메서드를 통해 쉽게 알 수 있다.
- switch를 이용해 맞는 개수(`bestCnt`, `worstCnt`)를 등수에 매칭시켜 줬는데, 맞은 개수에 따른 등수 배열을 만들면 index로 값을 매칭시킬 수 있어서 훨신 코드가 간결해진다.

    맞은 개수가 0개, 1개일 때 6등, 2개 5등, 3개 4등, ..., 6개 1등이 된다.


## 전체 코드
{% capture code %}
{% highlight java linenos %}
import java.util.ArrayList;
import java.util.Arrays;

class Solution {
  public int[] solution(int[] lottos, int[] win_nums) {
    //lottos[] = 구매한 로또 번호를 담은 배열
    //win_nums[] = 당첨 번호를 담은 배열
    int bestCnt = 0; // 최대로 일치하는 개수
    int worstCnt = 0; // 최저로 일치하는 개수
    int[] prize = new int[] {6, 6, 5, 4, 3, 2, 1}; // 맞은 개수에 따른 점수
    //////////////////////// 0, 1, 2, 3, 4, 5, 6 // 맞은 개수

    ArrayList<Integer> list = new ArrayList<>(); // 0이 아닌 번호 저장

    for (int lotto : lottos) { // 구매한 로또 번호
      if (lotto == 0) { // 알아볼 수 없는 번호일 때
        bestCnt++;
      } else {
        list.add(lotto);				
      }
    }

    for (int num : win_nums ) {
      if (list.contains(num)) {
        bestCnt++;
        worstCnt++;
      }
    }

    return new int[] {prize[bestCnt], prize[worstCnt]};
  }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## 참고
- 
{: .mb-10 }