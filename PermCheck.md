# PermCheck

## 문제

A non-empty array A consisting of N integers is given.

A permutation is a sequence containing each element from 1 to N once, and only once.

For example, array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
    A[3] = 2
    
is a permutation, but array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
    
is not a permutation, because value 2 is missing.

The goal is to check whether array A is a permutation.

Write a function:

> class Solution { public int solution(int[] A); }

that, given an array A, returns 1 if array A is a permutation and 0 if it is not.

For example, given array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
    A[3] = 2
    
the function should return 1.

Given array A such that:

    A[0] = 4
    A[1] = 1
    A[2] = 3
    
the function should return 0.

Write an efficient algorithm for the following assumptions:

* N is an integer within the range [1..100,000];
* each element of array A is an integer within the range [1..1,000,000,000].

_Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited._

## 풀이

``` java
import java.util.*;

public class Main {
	public static void main(String[] args) {
		int[] A = {4, 1, 3, 2};
		System.out.println(solution(A));
	}
	
	public static int solution(int[] A) {
		Arrays.sort(A);
		
		for (int i = 1; i <= A.length; i++) {
			if (A[i - 1] != i) {
				return 0;
			}
		}
		
		return 1;
	}
}
```

## 문제 해결 방법

* 처음에는 배열과 리스트를 사용했지만 메모리 초과와 시간 초과 문제가 생겼음
* 배열을 **정렬**한 뒤 비교하여 
