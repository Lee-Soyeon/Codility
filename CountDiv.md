# CountDiv

## 문제

Write a function:

> class Solution { public int solution(int A, int B, int K); }

that, given three integers A, B and K, returns the number of integers within the range [A..B] that are divisible by K, i.e.:

> { i : A ≤ i ≤ B, i mod K = 0 }

For example, for A = 6, B = 11 and K = 2, your function should return 3, because there are three numbers divisible by 2 within the range [6..11], namely 6, 8 and 10.

Write an efficient algorithm for the following assumptions:

* A and B are integers within the range [0..2,000,000,000];
* K is an integer within the range [1..2,000,000,000];
* A ≤ B.

_Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited._

## 해석

* A부터 B까지의 범위 중 K로 나누어 떨어지는 숫자의 개수를 세는 문제

## 풀이

``` java

public class Main {
	public static void main(String[] args) {
		System.out.println(solution(6, 11, 2));
	}

	public static int solution(int A, int B, int K) {
		if (A == 0) {
			return B / K + 1;
		} else {
			return B / K - (A - 1) / K;
		}
	}
}
```

## 문제 해결 방법

* 처음에는 for문에서 i의 범위를 A부터 B까지로 설정하고 i가 K로 나누어 떨어지는 횟수를 셌으나 **시간 초과**
* 누적 합(Prefix Sums) 개념에 대해 공부함
* B를 K로 나눈 몫에서 (A - 1)을 K로 나눈 몫을 뺌

