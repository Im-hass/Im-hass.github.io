---
layout: default
title: Javascript | Lv1. 숫자 문자열과 영단어
parent: Programmers
grand_parent: Coding Test
permalink: /docs/coding-test/programmers/Javascript_Lv1_숫자_문자열과_영단어
# nav_order: 4
---

# Lv1. 숫자 문자열과 영단어

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/81301)

Javascript
{: .label .mt-3 }

Lv1
{: .label .label-purple }

Success
{: .label .label-green }

## 문제
- 일부 자릿수를 영단어로 바꾼 카드를 건네주면 원래 숫자를 찾는 게임
  - 일부 자릿수를 영단어로 바꾸는 예시 1478 → "one4seveneight"
- 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어질 때, s가 의미하는 원래 숫자를 return한다.
- s가 "zero" 또는 "0"으로 시작하는 경우는 주어지지 않는다.

## 접근 방법
1. 영어 배열을 돌며 해당 **영어를 숫자(인덱스)로 replace**한다.
2. 여기서 "oneone" 같은 문자열이 주어질 경우, "one" 전부를 replace해줘야 하므로 정규식을 이용하여 `g` 옵션을 준다.

## 주의 사항
- 정규식을 사용하면 편하게 풀 수 있다. [정규식 참고](https://im-hass.github.io/docs/javascript/grammar/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D_%EC%A0%95%EA%B7%9C%EC%8B%9D)
- 정규식에 변수와 옵션을 사용하는 방법을 알아야 한다.
  **RegExp 객체를 생성**해야 변수를 쓸 수 있다.
  **옵션은 두번째** 매개변수로 전달한다.

## 전체 코드
{% capture code %}
{% highlight javascript linenos %}
function solution(s) {
  let eng = ['zero', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];
  
  for (let i = 0; i < eng.length; i++) {
    const regex = new RegExp(`${eng[i]}`, "g");
    s = s.replace(regex, i);
  }
  
  return parseInt(s);
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## 참고
- 
{: .mb-10 }