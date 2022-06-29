---
layout: default
title: Java | Lv1. 실패율
parent: Programmers
grand_parent: Coding Test
permalink: /docs/coding-test/programmers/Java_Lv1_실패율
nav_order: 3
---

# Lv1. 실패율
{: .fw-500 }

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/92334)

Java
{: .label .mt-3 }

Lv1
{: .label .label-purple }

Failed
{: .label .label-red }

## 문제
- **실패율 :** 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수
- **N :** 전체 스테이지의 개수
- **stages :** 게임을 이용하는 사용자가 현재 멈춰있는 스테이지의 번호가 담긴 배열
- N + 1 은 마지막 스테이지(N 번째 스테이지) 까지 클리어 한 사용자
- 스테이지에 도달한 유저가 없는 경우 해당 스테이지의 실패율은 **0으로 정의**한다.
- 실패율이 같은 스테이지가 있다면 작은 번호의 스테이지가 먼저 오도록 정렬한다.
- **실패율이 높은 스테이지부터 내림차순**으로 스테이지의 번호가 담겨있는 배열을 return한다.

## 접근 방법
1. 1 ~ N 스테이지까지 반복하며 stages 배열에서 해당 스테이지를 클리어 못한 플레이어와 클리어 한 플레이어를 센다.
2. 클리어 못한 플레이어와 클리어한 플레이어가 스테이지에 도달한 전체 플레이어 수가 된다.
3. 클레이어 못한 플레이어를 전체 플레이어 수로 나누어 실패율을 구한다.
4. 만약 클리어 못한 플레이어와 클리어한 플레이어가 0이라면(스테이지에 도달한 유저가 없는 경우) 실패율은 0으로 정의한다.
5. 스테이지와 실패율을 객체에 저장한다.
6. 스테이지 끝까지 확인했다면 실패율을 기준으로 객체를 정렬한다.

## 주의 사항
- **객체**를 사용하면 쉽게 풀 수 있는 문제이다.
- 클리어 못 한 플레이어와 스테이지에 도달한 플레이어가 0명이면 **0/0 이라서 NaN**이 나온다.

## 전체 코드
{% capture code %}
{% highlight java linenos %}
import java.util.ArrayList;
import java.util.Collections;

class Solution {
  static class Rate { // 스테이지와 실패율을 저장하는 객체
    int idx; // stage number
    double rate; // fail rate

    public Rate(int idx, double rate) {
        this.idx = idx;
        this.rate = rate;
    }
  }
  
  public int[] solution(int N, int[] stages) {
    int[] answer = new int[N];
    ArrayList<Rate> arr = new ArrayList<>();
    // double[][] fail = new double[N][2]; // 실패율, [스테이지][스테이지, 실패율]
    
    for (int i = 1; i <= N; i++) {
        int no = 0; // 스테이지 도달, 클리어 못한 플레이어
        int yes = 0; // 스테이지 도달, 클리어 한 플레이어
        
        for (int stage : stages) {
            if (stage == i) { // 스테이지에 도달, 클리어 못한 플레이어
                no++;
            } else if (stage > i) { // 스테이지 도달, 클리어 한 플레이어
                yes++;
            }
        }
        
        double total = yes + no; // 스테이지에 도달한 플레이어 수
        double fail = no / total;
        if (no == 0 && total == 0.0) {
            fail = 0;
        }
        arr.add(new Rate(i, fail));
    }
    
    Collections.sort(arr, ((r1, r2) -> Double.compare(r2.rate, r1.rate)));
    
    int idx = 0;
    for (Rate i : arr) {
        answer[idx] = i.idx;
        idx++;
    }
    
    return answer;
  }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## 참고
- 
{: .mb-10 }