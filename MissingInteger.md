# MissingInteger

## 문제

This is a demo task.

Write a function:

> class Solution { public int solution(int[] A); }

that, given an array A of N integers, returns the smallest positive integer (greater than 0) that does not occur in A.

For example, given A = [1, 3, 6, 4, 1, 2], the function should return 5.

Given A = [1, 2, 3], the function should return 4.

Given A = [−1, −3], the function should return 1.

Write an efficient algorithm for the following assumptions:

* N is an integer within the range [1..100,000];
* each element of array A is an integer within the range [−1,000,000..1,000,000].

_Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited._

## 풀이

``` java

public class Main {
	public static void main(String[] args) {
		int[] A = {1, 2, 3};
		System.out.println(solution(A));
	}
	
	public static int solution(int[] A) {
		int[] result = new int[1000001];
		
		for (int i = 0; i < A.length; i++) {
			if (A[i] >= 0) {
				result[A[i]] = 1;
			}
		}
		
		for (int i = 1; i < result.length; i++) {
			if (result[i] == 0) {
				return i;
			}
		}
		
		return 0;
	}
}
```

## 문제 해결 방법

* 각 원소의 범위가 [−1,000,000..1,000,000]였고 음수는 신경쓰지 않아도 되기 때문에 배열을 이용하여 풀었음
* HashSet을 이용하여 풀 수도 
