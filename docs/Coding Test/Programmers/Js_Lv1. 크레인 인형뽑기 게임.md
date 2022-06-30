---
layout: default
title: Javascript | Lv1. 크레인 인형뽑기 게임
parent: Programmers
grand_parent: Coding Test
permalink: /docs/coding-test/programmers/Javascript_Lv1_크레인_인형뽑기_게임
# nav_order: 4
---

# Javascript | Lv1. 크레인 인형뽑기 게임

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64061)

Javascript
{: .label .mt-3 }

Lv1
{: .label .label-purple }

Success
{: .label .label-green }

## 문제
- 게임 화면은 "1 x 1" 크기의 칸들로 이루어진 "N x N" 크기의 정사각 격자이다.
- 위쪽에는 크레인이 있고 오른쪽에는 바구니가 있다.
- 각 격자 칸에는 다양한 인형이 들어 있으며 인형이 없는 칸은 빈칸이다.
- 모든 인형은 "1 x 1" 크기의 격자 한 칸을 차지하며 격자의 가장 아래 칸부터 차곡차곡 쌓여 있다.
- 인형은 1 ~ 100의 숫자로 나타내며 같은 숫자는 같은 모양의 인형을 나타낸다.
- 게임 사용자는 크레인을 좌우로 움직여서 멈춘 위치에서 가장 위에 있는 인형을 집어 올릴 수 있다.
- 집어 올린 인형은 바구니에 쌓이게 되는 데, 이때 바구니의 가장 아래 칸부터 인형이 순서대로 쌓이게 된다.
- 만약 같은 모양의 인형 두 개가 바구니에 연속해서 쌓이게 되면 두 인형은 터뜨려지면서 바구니에서 사라진다.
- 만약 인형이 없는 곳에서 크레인을 작동시키는 경우에는 아무런 일도 일어나지 않습니다.
- 크레인을 모두 작동시킨 후 터트려져 사라진 인형의 개수를 return한다.

## 접근 방법
{% capture code %}
{% highlight javascript linenos %}
moves 배열을 하나씩 탐색한다. (x좌표 = moves[i] - 1)
    0 ~ N까지 y좌표를 탐색한다.
        만약 0이 아니라면(인형이 있다면)
            바구니에 인형을 넣는다.
            해당 좌표[y, x]를 빈칸(0)으로 바꾼다.
            y좌표 탐색 종료

    바구니의 길이가 2 이상일 때
        바구니의 마지막 2개를 비교하여 인형이 2개 연속 쌓였는지 확인한다
        만약 2개가 같다면
            2개를 꺼내기
            터진개수 + 2
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## 주의 사항
- 

## 전체 코드
{% capture code %}
{% highlight javascript linenos %}
function solution(board, moves) {
  // board : 게임 화면, 격자의 상태가 담긴 2차원 배열
  // moves : 인형을 집기 위해 크레인을 작동시킨 위치가 담긴 배열
  let answer = 0;
  let basket = [];
  for (let i = 0; i < moves.length; i++) { // moves 배열을 하나씩 탐색한다. (x좌표 = moves[i] - 1)
    let x = moves[i] - 1;
    for (let y = 0; y < board.length; y++) { // 0 ~ N까지 y좌표를 탐색한다.
      if (board[y][x] != 0) { // 만약 0이 아니라면(인형이 있다면)
        basket.push(board[y][x]); // 바구니에 인형을 넣는다.
        board[y][x] = 0; // 해당 좌표[y, x]를 빈칸(0)으로 바꾼다.
        break; // y좌표 탐색 종료
      }
    }
    
    if (basket.length >= 2) { // 바구니의 길이가 2 이상일 때
      let idx = basket.length - 1;
      // 바구니의 마지막 2개를 비교하여 인형이 2개 연속 쌓였는지 확인한다
      if (basket[idx] == basket[idx - 1]) { // 2개가 같다면
        basket.length = basket.length - 2; // 2개를 꺼내기
        answer += 2; // 터진개수 + 2
      }
    }
  }

  return answer;
}
{% endhighlight %}
{% endcapture %}
{% include fix_linenos.html code=code %}
{% assign code = nil %}

## 참고
- 
{: .mb-10 }