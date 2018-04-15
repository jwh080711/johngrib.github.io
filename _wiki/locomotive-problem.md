---
layout  : wiki
title   : 기관차 문제(locomotive problem)
summary : 기관차 한 대의 번호를 보고 전체 기관차 수를 추정하자
date    : 2018-04-14 12:04:06 +0900
updated : 2018-04-14 19:24:37 +0900
tags    : bayes
toc     : true
public  : true
parent  : problem
latex   : true
---
* TOC
{:toc}

# 개요

* 이 문서는 [[Think-Bayes]] 책 43~45쪽을 공부한 내용이다.
* 프레드릭 모스텔러(Frederick Mosteller)의 "모스텔러의 확률 고급 문제 50선과 해답"을 보면 기관차 문제가 있다.

>
각 철도에는 이를 지나가는 기관차에 1부터 N까지의 순서로 번호를 붙인다.
어느날 60호 기관차를 보았다.
이 때 이 철도에는 몇 개의 기관차가 지나가는지 추측해보자.

# 풀이

## 가설 세우기

이 문제는 [[dice-problem]]과 비슷하다.

주사위 문제의 풀이를 활용하기 위해 문제를 다음과 같이 생각할 수 있다.

* 60 면체, 60 + 1 면체, 60 + 2 면체, ... 60 + n 면체 주사위가 든 상자가 있다.
* 상자에서 임의로 주사위 하나를 집어서 던졌더니 `60`이 나왔다.
* 각 주사위를 선택했을 확률은?

가설과 데이터는 어떻게 될까?

* n 개의 가설(Hypothesis)을 생각할 수 있다.
    * 가설 60 : 60면체 주사위를 던졌다.
    * 가설 61 : 61면체 주사위를 던졌다.
    * ...
    * 가설 n : n 면체 주사위를 던졌다.
* 데이터 D : 주사위를 던져 `60`이 나왔다.

표로 정리해 보면 다음과 같을 것이다.

| 식                   | 설명                                          | 값                 |
|----------------------|-----------------------------------------------|--------------------|
| $$p(H_{60})$$        | n개의 주사위 중 60면체 주사위를 선택할 확률   | $$\frac{1}{n}$$    |
| $$p(H_{61})$$        | n개의 주사위 중 61면체 주사위를 선택할 확률   | $$\frac{1}{n}$$    |
| ...                  | ...                                           | ...                |
| $$p(H_n)$$           | n개의 주사위 중 n면체 주사위를 선택할 확률    | $$\frac{1}{n}$$    |
| $$p(H_{1000})$$      | 1000개의 주사위 중 n면체 주사위를 선택할 확률 | $$\frac{1}{1000}$$ |
| $$p(D \mid H_{60})$$ | 60면체 주사위를 던져 60이 나올 확률           | $$\frac{1}{60}$$   |
| $$p(D \mid H_{61})$$ | 61면체 주사위를 던져 60이 나올 확률           | $$\frac{1}{61}$$   |
| ...                  | ...                                           | ...                |
| $$p(D \mid H_{x})$$  | x면체 주사위를 던져 60이 나올 확률            | $$\frac{1}{x}$$    |
| $$p(D)$$             | 주사위를 던져 60이 나올 확률                  | 아직 모름          |

## p(D)를 구하자

$$p(D)$$의 개념은 다음과 같다.

$$
\begin{align}
p(D) = & \space p(D \space and \space H_{60}) \\
        & + p(D \space and \space H_{61}) \\
        & + ... \\
        & + p(D \space and \space H_{n}) \\
\end{align}
$$

따라서 `60`면체에서 `m`면체까지 주사위가 전부 `m - 59` 개 있을 때,
$$p(D)$$는 다음과 같다.

$$
\begin{align}
p(D) = & \space p(H_{m-59})p(D \mid H_{60}) \\
        & + p(H_{m-59})p(D \mid H_{61}) \\
        & + ... \\
        & + p(H_{m-59})p(D \mid H_{m}) \\
\\
    = & \space \frac{1}{m-59} \times \frac{1}{60} \\
        & + \frac{1}{m-59} \times \frac{1}{61} \\
        & + ... \\
        & + \frac{1}{m-59} \times \frac{1}{m} \\
\\
    = & \space \lim_{m \to \infty} \frac{1}{m-59} \left( \frac{1}{60} + \frac{1}{61} + ... + \frac{1}{m} \right) \\
    = & \lim_{m \to \infty} \frac{1}{m-59} \sum_{k = 60}^{m} k^{-1} \\
\end{align}
$$

한편, $$\sum_{k = 60}^{m} k^{-1}$$는 [조화수(Harmonic number)](https://ko.wikipedia.org/wiki/%EC%A1%B0%ED%99%94%EC%88%98 ) $$H_m$$ 이므로 이를 써서 다시 표기해보면 다음과 같이 표현할 수 있다.

$$p(D) = \lim_{m \to \infty} \frac{1}{m-59} \times \left( H_m - H_{59} \right)$$

그런데, n이 너무 커지면 곤란하기도 하고, 현실의 열차가 무한히 많을 수는 없으니 편의상 1000 까지만 따져 보도록 하자.

$$p(D) = \frac{1}{1000 - 59} \times \left( H_{1000} - H_{59} \right)$$

손으로 계산하기엔 시간이 너무 걸리므로 다음과 같이 간단한 자바스크립트 함수를 작성하여 계산해주자.

```javascript
// 조화수 H_n 을 구한다
function harmonic(n) {
    if (n < 1) {
        throw "invalid argument";
    }
    if (harmonic[n] != null) {
        return harmonic[n];
    }
    if (n == 1) {
        return harmonic[1] = 1;
    }
    return harmonic[n] = harmonic(n - 1) + Math.pow(n, -1);
}
const p_d = (harmonic(1000) - harmonic(59)) / (1000 - 59);
console.log(p_d);
```

위의 코드를 실행해보면 다음과 같은 값이 출력된다.

$$p(D) \approx 0.0029992211628748922$$



## 사후 확률을 계산하자

이제 사후 확률을 계산할 수 있다.

[[Bayes-theorem]]에 의해 사후 확률은 다음과 같다. (단, $$ x \ge 60$$)

$$
\begin{align}
p(H_n \mid D) & = {p(H_n) \times p(D \mid H_n) \over p(D)} \\
    & = {\frac{1}{1000-59} \times \frac{1}{n} \over p(D)} \\
    & = {1 \over (1000-59) \times n \times p(D)}\\
    & = {1 \over 941 \times n \times p(D)}\\
\end{align}
$$


그렇다면 이제 모든 가설(열차가 60 대인 경우, 61 대인 경우, ... n 대인 경우)을 비교하여 가장 가능성이 높은 가설을 찾아내기만 하면 된다.

즉, 다음 값들을 비교하여 가장 큰 값을 찾으면 된다.

$$
\begin{matrix}
p(H_{60} \mid D), & p(H_{61} \mid D), & ...
\end{matrix}
$$

그런데 `n`이 분모에 있으므로, `n`이 커질수록 수는 작아진다.

따라서 가능한 확률의 최대값이 나오는 n 은 `60`이 된다.

당연히 `60대 중의 1대일 가능성`이 `61대 중의 1대일 가능성`이나, `62대 중의 1대일 가능성`보다 크기 때문이다.



## 기대값을 구해보자

하지만 원하는 값은 이런 결과가 아니므로, 관점을 바꾸어 기대값을 구해 보도록 하자.

$$
\begin{align}
& 60 \times p(H_{60} \mid D) + 61 \times p(H_{61} \mid D) + ... + 1000 \times p(H_{1000} \mid D) \\
& = \frac{60}{941 \times 60 \times p(D)} + \frac{61}{941 \times 61 \times p(D)} + ... + \frac{1000}{941 \times 1000 \times p(D)} \\
& = \frac{1}{941 \times p(D)} + \frac{1}{941 \times p(D)} + ... + \frac{1}{941 \times p(D)} \\
& = 941 \times \frac{1}{941 \times p(D)} \\
& = \frac{1}{p(D)} \\
& \approx \frac{1}{0.0028222671142652737} \\
& \\
& \approx 333.41989326370776 \\
\end{align}
$$

즉, 333대의 열차가 있을 것이라고 기대할 수 있다.



### 기대값을 구하는 공식을 만들어 보자

$$1 \over p(D)$$를 이용하면 되므로 공식으로도 만들 수 있을 것 같다.

* a : 목격한 열차의 번호
* b : 임의의 열차 번호 예상 최대값(위에서 1000으로 사용한 값)

$$
\begin{align}
\frac{1}{p(D)} & = \left( \frac{1}{b - (a - 1) } \times \left( H_b - H_{a - 1} \right) \right)^{-1}\\
    & \\
    & = {b - (a - 1) \over \sum_{k = a}^{b} k^{-1} } \\
\end{align}
$$


### WolframAlpha에 물어보자

공식을 만들었으니, 언제든지 WolframAlpha에 물어볼 수 있다.


{% raw %}
<div id="locomotive-search">
    <div>a = <input type="number" value="60" id="locomotive-a"/></div>
    <div>b = <input type="number" value="1000" id="locomotive-b"/></div>
    <div><input type="button" value="WolframAlpha에 물어보기" onClick="wolfram()"/></div>
</div>
{% endraw %}


# Links

* [[Think-Bayes]]
* [Fifty Challenging Problems in Probability with Solutions By Frederick Mosteller](http://store.doverpublications.com/0486653552.html )
* [조화수(wikipedia)](https://ko.wikipedia.org/wiki/%EC%A1%B0%ED%99%94%EC%88%98 )

{% raw %}
<script>
function wolfram() {

    var a = parseInt(document.getElementById('locomotive-a').value, 10);
    var b = parseInt(document.getElementById('locomotive-b').value, 10);
    var c = a - 1;

    var url = 'https://www.wolframalpha.com/input/?i=(' + b + '-' + c + ')%2F(harmonic+number+' + b + '+-+harmonic+number+' + c + ')';

    window.open(url, '_blank');
}
</script>
{% endraw %}