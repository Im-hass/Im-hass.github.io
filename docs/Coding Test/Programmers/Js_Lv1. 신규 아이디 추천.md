---
layout: default
title: Javascript | Lv1. 신규 아이디 추천
parent: Programmers
grand_parent: Coding Test
permalink: /docs/coding-test/programmers/Js_Lv1_신규아이디추천
# nav_order: 4
---

# Lv1. 신규 아이디 추천

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/72410)

Javascript
{: .label .mt-3 }

Lv1
{: .label .label-purple }

Success
{: .label .label-green }

## 문제
- 문제 그대로하면 되는 구현 문제이다.
- 카카오 아이디 규칙에 맞지 않는 아이디를 입력했을 때, 입력된 아이디와 유사하면서 규칙에 맞는 아이디를 return해준다.
- 카카오 아이디의 규칙 :
  - 아이디의 길이는 3자 이상 15자 이하여야 합니다.
  - 아이디는 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.) 문자만 사용할 수 있습니다.
  - 단, 마침표(.)는 처음과 끝에 사용할 수 없으며 또한 연속으로 사용할 수 없습니다.

- 아래 7단계의 순차적인 처리 과정을 통해 신규 유저가 입력한 아이디가 카카오 아이디 규칙에 맞는 지 검사하고 규칙에 맞지 않은 경우 규칙에 맞는 새로운 아이디를 추천해준다.
  - 1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.
  - 2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
  - 3단계 new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환합니다.
  - 4단계 new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거합니다.
  - 5단계 new_id가 빈 문자열이라면, new_id에 "a"를 대입합니다.
  - 6단계 new_id의 길이가 16자 이상이면, new_id의 첫 15개의 문자를 제외한 나머지 문자들을 모두 제거합니다.
      만약 제거 후 마침표(.)가 new_id의 끝에 위치한다면 끝에 위치한 마침표(.) 문자를 제거합니다.
  - 7단계 new_id의 길이가 2자 이하라면, new_id의 마지막 문자를 new_id의 길이가 3이 될 때까지 반복해서 끝에 붙입니다.

## 접근 방법
- 정규식을 사용하면 편하게 풀 수 있다. [정규식 참고](https://im-hass.github.io/docs/javascript/grammar/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D_%EC%A0%95%EA%B7%9C%EC%8B%9D)
- 순서대로 하나씩 구현해나간다.
- 메소드 체이닝을 사용하면 더 보기 좋게 구현할 수 있다.

## 주의 사항
-

## 전체 코드
{% capture code %}
{% highlight javascript linenos %}
function solution(new_id) {
    var answer = new_id;
    const upperReg = /[A-Z]/;
    const symbolReg = /[~|!|@|#|$|%|^|&|*|(|)|=|+|[|\]|{|}|:|?|,|<|>|\/]/; // ~!@#$%^&*()=+[{]}:?,<>/
    
    if (new_id.length < 3 || new_id.length > 15 ||
        new_id[0] === "." || new_id[new_id.length - 1] === "." ||
        upperReg.test(new_id) ||
        symbolReg.test(new_id)) {
        // id 길이가 3보다 작거나 15보다 클 경우
        // 처음이나 끝에 마침표가 들어갈 경우
        // 대문자가 있을 경우
        // 허용되지 않는 특수문자가 들어갈 경우
        answer = changeId(new_id);
    }
    
    return answer;
}

function changeId(id) {
  // 1단계 모든 대문자 -> 소문자로 치환
  id = id.toLowerCase();
  
  // 2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
  id = id.replace(/[~|!|@|#|$|%|^|&|*|(|)|=|+|[|\]|{|}|:|?|,|<|>|\/]/g, "");
  
  // 3단계 new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환합니다.
  id = id.replace(/[.]{2,}/g, ".");
  
  // 4단계 new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거합니다.
  id = id.replace(/^[.]|[.]$/g, "");
  
  // 5단계 new_id가 빈 문자열이라면, new_id에 "a"를 대입합니다.
  if (id.length === 0) id += "a";
  
  // 6단계 new_id의 길이가 16자 이상이면, new_id의 첫 15개의 문자를 제외한 나머지 문자들을 모두 제거합니다.
  //      만약 제거 후 마침표(.)가 new_id의 끝에 위치한다면 끝에 위치한 마침표(.) 문자를 제거합니다.
  if (id.length >= 16) id = id.slice(0, 15).replace(/[.]$/g, "");
  
  // 7단계 new_id의 길이가 2자 이하라면, new_id의 마지막 문자를 new_id의 길이가 3이 될 때까지 반복해서 끝에 붙입니다.
  if (id.length <= 2) {
    let add = id[id.length - 1];
    while (id.length < 3) {
      id += add;
    }
  }
  
  return id;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## 다른 사람 풀이
- 정규식, repeat
{% capture code %}
{% highlight javascript linenos %}
function solution(new_id) {
    const answer = new_id
        .toLowerCase() // 1
        .replace(/[^\w-_.]/g, '') // 2
        .replace(/\.+/g, '.') // 3
        .replace(/^\.|\.$/g, '') // 4
        .replace(/^$/, 'a') // 5
        .slice(0, 15).replace(/\.$/, ''); // 6
    const len = answer.length;
    return len > 2 ? answer : answer + answer.charAt(len - 1).repeat(3 - len);
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

- 정규 표현식만 사용
{% capture code %}
{% highlight javascript linenos %}
const solution = new_id =>
    new_id.toLowerCase()
          .replace(/[^\w-_.]/g, "")
          .replace(/\.+/g, ".")
          .replace(/^\.|\.$/g, "")
          .replace(/^$/, "a")
          .match(/^.{0,14}[^.]/)[0]
          .replace(/^(.)$/, "$1$1$1")
          .replace(/^(.)(.)$/, "$1$2$2");
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## 참고
- 
{: .mb-10 }