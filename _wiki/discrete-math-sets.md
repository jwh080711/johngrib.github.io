---
layout  : wiki
title   : 집합
summary : Sets
date    : 2019-01-14 22:13:18 +0900
updated : 2019-01-19 18:12:27 +0900
tags    : math
toc     : true
public  : true
parent  : study-discrete-mathematics
latex   : true
---
* TOC
{:toc}

# 정의

## 집합(sets)

>
A set is an unordered collection of objects, called elements or members of the set.
A set is said to contain its elements.
We write $$a ∈ A$$ to denote that a is an element of the set A.
The notation $$a \notin A$$ denotes that a is not an element of the set A.

* 집합은 순서 없는 객체들의 컬렉션이다.

## 집합의 같음

>
Two sets are equal if and only if they have the same elements.
Therefore, if A and B are sets,
then A and B are equal if and only if $$∀x(x ∈ A ↔ x ∈ B)$$.
We write $$A=B$$ if A and B are equal sets.

* 두 집합이 같은 원소를 갖고 있다면 두 집합은 같다.
* $$ A \subseteq B $$ 이고, $$ B \subseteq A $$ 이면 $$ A=B $$.

## 부분집합(subset), 진 부분집합(proper subset)

>
The set A is a subset of B if and only if every element of A is also an element of B.
We use the notation $$A ⊆ B$$ to indicate that A is a subset of the set B.

* 집합 A의 모든 원소가 집합 B의 원소이면 A는 B의 부분집합이다.
* $$ A \subset B $$ : 진 부분집합(proper subset)
    * $$ A \subseteq B $$ 이고, $$ A \ne B $$ 이면 A는 B의 진 부분집합.

## 집합의 크기(cardinality)

>
Let S be a set.
If there are exactly n distinct elements in S where n is a nonnegative integer,
we say that S is a finite set and that n is the cardinality of S.
The cardinality of S is denoted by $$ \vert S \vert $$.

* 유한 집합(finite set) S의 크기는 $$ \vert S \vert $$로 표기한다.

## 멱집합(poser set)

>
Given a set S, the power set of S is the set of all subsets of the set S.
The power set of S is denoted by $$P(S)$$.

* 집합 S의 멱집합(power set)은 집합 S의 모든 부분집합의 집합을 말한다.
* $$ P(S) $$로 표기한다.

## 데카르트 곱(cartesian products)

>
Let A and B be sets.
The Cartesian product of A and B, denoted by $$A × B$$,
is the set of all ordered pairs $$(a, b)$$, where $$a ∈ A$$ and $$b ∈ B$$.
Hence, $$A × B = \{(a, b) \vert a ∈ A ∧ b ∈ B \}$$

* A와 B의 데카르트 곱 $$A × B$$는 $$a ∈ A$$ 이고 $$b ∈ B$$인 모든 순서쌍의 집합이다.
* $$ A_1 × A_2 × ... × A_n = \{(a_1, a_2, ..., a_n) \vert a_i ∈ A_i \ for \ i = 1, 2, ..., n \} $$ &nbsp;
* $$ A × B $$의 부분집합 $$ R $$을 집합 A 로부터 집합 B로의 관계(relation)라고 한다.

## 연산

### 합집합(union)

> Let A and B be sets.
The union of the sets A and B, denoted by $$A ∪ B$$,
is the set that contains those elements that are either in A or in B, or in both.

* $$ A ∪ B = \{ x \vert x ∈ A ∨ x ∈ B \} $$
* 여러 집합의 합집합은 적어도 하나의 집합에 있는 원소들의 집합이다.

$$ A_1 ∪ A_2 ∪ ... ∪ A_n = \bigcup_{i=1}^n A_i $$

### 교집합(intersection)

> Let A and B be sets.
The intersection of the sets A and B, denoted by $$A ∩ B$$,
is the set containing those elements in both A and B.

* $$ A ∩ B = \{ x \vert x ∈ A ∧ x ∈ B \} $$
* 여러 집합의 교집합은 여러 집합 모두에 나타나는 원소들의 집합이다.

$$ A_1 ∩ A_2 ∩ ... ∩ A_n = \bigcap_{i=1}^n A_i $$

#### 서로 소(disjoint)

> Two sets are called disjoint if their intersection is the empty set.

* 두 집합의 교집합이 공집합인 경우를 서로 소라 한다.

### 차집합(difference)

> Let A and B be sets. The difference of A and B, denoted by $$A − B$$, is the set containing those elements that are in A but not in B. The difference of A and B is also called the complement of B with respect to A.

* A에 대한 B의 여집합(complement of B with respect to A) 이라고도 부른다.
* $$ A-B = \{ x \vert x ∈ A ∧ x ∉ B \} $$

### 여집합(complement)

> Let U be the universal set. The complement of the set A, denoted by $$ \bar{A} $$, is the complement of A with respect to U . Therefore, the complement of the set A is $$U − A$$.

* 여집합은 $$ U - A $$이고, $$ \bar{A} $$로 표기한다.
* $$ \bar{A} = \{ x ∈ U \vert x ∉ A \} $$

# 용어 정리

| English                    | 한국어          | Example                                            |
|----------------------------|-----------------|----------------------------------------------------|
| element, member            | 원소            |                                                    |
| roster method              | 원소나열법      | $$ O = \{ 1,2,3 \} $$                              |
| set builder notation       | 조건 제시법     | $$ O = \{ x \vert x\text{는 짝수} \} $$            |
| empty set, null set        | 공집합          | $$ \emptyset $$                                    |
| singleton set              | 단일원소 집합   | $$ O = \{ 1 \} $$                                  |
| venn diagrams              | 벤 다이어그램   |                                                    |
| universal set              | 전체집합        | $$ U $$                                            |
| subsets                    | 부분집합        |                                                    |
| proper subset              | 진부분집합      |                                                    |
| size of a set, cardinality | 집합의 크기     | $$ \vert \emptyset \vert = 0 $$                    |
| power set                  | 멱집합          | $$ P(\{0,1\})=\{\emptyset,\{0\},\{1\},\{0,1\}\} $$ |
| ordered n-tuples           | 순서가 있는 n짝 |                                                    |
| ordered pairs              | 순서쌍          |                                                    |

## 조건 제시법의 예

| $$N =\{0,1,2,3,...\} $$                           | 자연수의 집합    | the set of natural numbers       |
| $$Z =\{...,-2,-1,0,1,2,...\} $$                   | 정수의 집합      | the set of integers              |
| $$Z^+=\{1,2,3,...\} $$                            | 양의 정수의 집합 | the set of positive integers     |
| $$Q =\{\frac{p}{q}\vert p\in Z,q\in Z,q\ne 0\} $$ | 유리수의 집합    | the set of rational numbers      |
| $$ R $$                                           | 실수의 집합      | the set of real numbers          |
| $$ R^+ $$                                         | 양의 실수의 집합 | the set of positive real numbers |
| $$ C $$                                           | 복소수의 집합    | the set of complex numbers       |

## 구간(interval) 표기법

$$
\begin{align}
[a,b] & = \{ x \vert a \le x \le b \} \\
[a,b) & = \{ x \vert a \le x \lt b \} \\
(a,b] & = \{ x \vert a \lt x \le b \} \\
(a,b) & = \{ x \vert a \lt x \lt b \} \\
\end{align}
$$

* **[a, b]** : 닫힌 구간(closed interval)
* **(a, b)** : 열린 구간(open interval)

# 집합의 항등

| $$A ∩ U = A$$ <br> $$A ∪ \emptyset = A $$                      | 항등법칙         | Identity laws       |
| $$A ∪ U = U$$ <br> $$A ∩ \emptyset = \emptyset $$              | 지배법칙         | Domination laws     |
| $$A ∪ A = A$$ <br> $$A ∩ A = A$$                               | 멱등법칙         | Idempotent laws     |
| $$ \overline{ (\bar{A}) } = A $$                               | 보원법칙         | Complementation law |
| $$A ∪ B = B ∪ A$$ <br> $$ A ∩ B = B ∩ A $$                     | 교환법칙         | Commutative laws    |
| $$A∪(B∪C) = (A∪B)∪C$$ <br> $$A∩(B∩C) = (A∩B)∩C$$               | 결합법칙         | Associative laws    |
| $$A∪(B∩C)=(A∪B)∩(A∪C)$$<br>$$A∩(B∪C)=(A∩B)∪(A∩C)$$             | 분배법칙         | Distributive laws   |
| $$\bar{A∩B}=\bar{A}∪\bar{B}$$<br>$$\bar{A∪B}=\bar{A}∩\bar{B}$$ | 드 모르간의 법칙 | De Morgan's laws    |
| $$A ∪ (A ∩ B) = A$$ <br> $$A ∩ (A ∪ B) = A $$                  | 흡수법칙         | Absorption laws     |
| $$A ∪ \bar{A} = U$$ <br> $$A ∩ \bar{A} = ∅ $$                  | 보수법칙         | Complement laws     |

# datatype 과 집합

>
컴퓨터과학에서 이야기하는 "데이터형"이라고 하는 개념은 집합의 개념 위에 정의된다는 것에 주목하라.
특히 **datatype, type**이란 집합과 그 집합을 구성하고 있는 개체에 적용할 수 있는 연산자들의 집합을 말한다.
예를 들어 boolean 이란 집합 $$ \{ 0, 1 \} $$과, 그 원소인 0과 1을 피연산자로 하여 연산을 수행하는
**AND, OR, NOT**과 같은 연산자들을 함께 지칭하는 것이다.

# 참고문헌

* Rosen의 이산수학 / Kenneth H. Rosen 저 / 공은배 등저 / 한국맥그로힐(McGraw-Hill KOREA) / 2017년 01월 06일
