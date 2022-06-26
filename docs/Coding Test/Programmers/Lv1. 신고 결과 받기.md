---
layout: default
title: Lv1. 신고 결과 받기
parent: Programmers
grand_parent: Coding Test
permalink: /docs/coding-test/programmers/Lv1_신고_결과_받기
nav_order: 1
---

# Lv1. 신고 결과 받기
{: .fw-500 }

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/92334)

Java
{: .label .mt-3 }

Lv1
{: .label .label-purple }

Failed
{: .label .label-red }

## 문제 풀이
- 각 유저는 한 번에 한 명의 유저를 신고할 수 있다.
- 신고 횟수는 제한이 없고, 서로 다른 유저를 계속해서 신고할 수 있다.
- 동일한 유저가 신고한 것은 1회로 처리한다.
- 모든 신고내용을 취합하여 마지막에 처리한다.
- k번 이상 신고된 유저는 게시판 이용이 정지된다.
- id_list에 담긴 id 순서대로 각 유저가 받은 결과 메일 수를 return한다.


## 주의 사항
- 자료 구조를 활용하면 쉽게 풀 수 있는 문제이다.
- set을 사용해 동일한 유저가 신고한 것은 1번만 저장하도록 한다.

## 전체 코드
{% capture code %}
{% highlight java linenos %}
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;

class Solution {
  public static int[] solution(String[] id_list, String[] report, int k) {
    int[] answer = new int[id_list.length];
    // id_list[] = 전체 유저 목록
    // report[] : "신고유저 신고당한유저", ...
    // k : k번 이상 신고되면 정지

    Map<String, HashSet<String>> map = new HashMap<>(); // <(key: 유저 id), (value: key를 신고한 사람(중복x))>
    Map<String, Integer> idxMap = new HashMap<>(); // <(key : 유저 id), (value: id_list에서 유저 index)>
    
    // Map 초기화
    for (int i = 0; i < id_list.length; i++) {
      String name = id_list[i];
      map.put(name, new HashSet<>()); // (유저 아이디, []) 추가
      idxMap.put(name, i); // (유저 아이디, 유저 인덱스) 추가
    }
    
    // 신고 기록 저장
    for (String s : report) {
      String[] str = s.split(" "); // [신고자 id, 신고한 id]
      String from = str[0]; // 신고자 id
      String to = str[1]; // 신고한 id
      map.get(to).add(from); // key(유저 id)를 찾아서 value(key를 신고한 사람)를 추가함.
    }
    
    // 이용 정지 메일 발송
    for (int i = 0; i < id_list.length; i++) {
      HashSet<String> send = map.get(id_list[i]); // 해당 유저를 신고한 사람들의 정보
      if (send.size() >= k) { // 해당 유저가 k번 이상 신고되었을 경우
        for (String name : send) {
          answer[idxMap.get(name)]++; // idxMap에서 해당 유저의 index를 가져와서 값을 증가
        }
      }
    }
    
    return answer;
  }
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## 참고
- [https://jangcenter.tistory.com/116](https://jangcenter.tistory.com/116)
{: .mb-10 }