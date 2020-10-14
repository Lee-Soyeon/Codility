# GenomicRangeQuery

## 문제

A DNA sequence can be represented as a string consisting of the letters A, C, G and T, which correspond to the types of successive nucleotides in the sequence. Each nucleotide has an impact factor, which is an integer. Nucleotides of types A, C, G and T have impact factors of 1, 2, 3 and 4, respectively. You are going to answer several queries of the form: What is the minimal impact factor of nucleotides contained in a particular part of the given DNA sequence?

The DNA sequence is given as a non-empty string S = S[0]S[1]...S[N-1] consisting of N characters. There are M queries, which are given in non-empty arrays P and Q, each consisting of M integers. The K-th query (0 ≤ K < M) requires you to find the minimal impact factor of nucleotides contained in the DNA sequence between positions P[K] and Q[K] (inclusive).

For example, consider string S = CAGCCTA and arrays P, Q such that:
```
    P[0] = 2    Q[0] = 4
    P[1] = 5    Q[1] = 5
    P[2] = 0    Q[2] = 6
```
The answers to these M = 3 queries are as follows:

* The part of the DNA between positions 2 and 4 contains nucleotides G and C (twice), whose impact factors are 3 and 2 respectively, so the answer is 2.
* The part between positions 5 and 5 contains a single nucleotide T, whose impact factor is 4, so the answer is 4.
* The part between positions 0 and 6 (the whole string) contains all nucleotides, in particular nucleotide A whose impact factor is 1, so the answer is 1.

Write a function:

> class Solution { public int[] solution(String S, int[] P, int[] Q); }

that, given a non-empty string S consisting of N characters and two non-empty arrays P and Q consisting of M integers, returns an array consisting of M integers specifying the consecutive answers to all queries.

Result array should be returned as an array of integers.

For example, given the string S = CAGCCTA and arrays P, Q such that:
```
    P[0] = 2    Q[0] = 4
    P[1] = 5    Q[1] = 5
    P[2] = 0    Q[2] = 6
```
the function should return the values [2, 4, 1], as explained above.

Write an efficient algorithm for the following assumptions:

* N is an integer within the range [1..100,000];
* M is an integer within the range [1..50,000];
* each element of arrays P, Q is an integer within the range [0..N − 1];
* P[K] ≤ Q[K], where 0 ≤ K < M;
* string S consists only of upper-case English letters A, C, G, T.

_Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited._

## 해석

* 문자 A,C,G,T는 각각 1,2,3,4로 대응함
* P[K]부터 Q[K]까지의 범위에서 문자에 대응하는 숫자 중 가장 작은 값을 구해야 함

## 풀이

``` java

public class Main {
	public static void main(String[] args) {
		String S = "CAGCCTA";
		int[] P = {2, 5, 0};
		int[] Q = {4, 5, 6};
		
		
		int[] result = solution(S, P, Q);
		for (int i = 0; i < result.length; i++) {
			System.out.print(result[i] + " ");
		}
	}

	public static int[] solution(String S, int[] P, int[] Q) {
		int[] A = new int[S.length() + 1];
		int[] C = new int[S.length() + 1];
		int[] G = new int[S.length() + 1];
		int[] T = new int[S.length() + 1];
		int[] result = new int[P.length];
		
		for (int i = 0; i < S.length(); i++) {
			if (S.charAt(i) == 'A') {
				A[i + 1] = A[i] + 1;
				C[i + 1] = C[i];
				G[i + 1] = G[i];
				T[i + 1] = T[i];
			}
			if (S.charAt(i) == 'C') {
				A[i + 1] = A[i];
				C[i + 1] = C[i] + 1;
				G[i + 1] = G[i];
				T[i + 1] = T[i];
			}
			if (S.charAt(i) == 'G') {
				A[i + 1] = A[i];
				C[i + 1] = C[i];
				G[i + 1] = G[i] + 1;
				T[i + 1] = T[i];
			}
			if (S.charAt(i) == 'T') {
				A[i + 1] = A[i];
				C[i + 1] = C[i];
				G[i + 1] = G[i];
				T[i + 1] = T[i] + 1;
			}
		}
		
		for (int i = 0; i < P.length; i++) {
			int a = A[Q[i] + 1] - A[P[i]];
			int c = C[Q[i] + 1] - C[P[i]];
			int g = G[Q[i] + 1] - G[P[i]];
			int t = T[Q[i] + 1] - T[P[i]];
			
			if (a > 0) {
				result[i] = 1;
			} else if (c > 0) {
				result[i] = 2;
			} else if (g > 0) {
				result[i] = 3;
			} else if (t > 0) {
				result[i] = 4;
			}
		}
		
		return result;
	}
}
```

## 문제 해결 방법

* 각 문자마다 배열을 선언하여 누적 합(Prefix Sums)를 구함
* 예를 들어, 배열 A는 첫 번째 for문을 통과한 뒤 {0, 0, 1, 1, 1, 1, 1, 2}의 값을 갖음 
* A[Q[i] + 1] - A[P[i]]가 0보다 크다면 P[i]부터 Q[i]까지의 범위 중 문자 A가 등장한 것
* 가장 작은 A부터 확인하여 범위 내의 최소값을 배열 result에 저장함
