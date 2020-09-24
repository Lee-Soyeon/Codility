# PermMissingElem

## 문제

An array A consisting of N different integers is given. The array contains integers in the range [1..(N + 1)], which means that exactly one element is missing.

Your goal is to find that missing element.

Write a function:

  * class Solution { public int solution(int[] A); }

that, given an array A, returns the value of the missing element.

For example, given array A such that:

> A[0] = 2, A[1] = 3, A[2] = 1, A[3] = 5

the function should return 4, as it is the missing element.

Write an __efficient__ algorithm for the following assumptions:

  * N is an integer within the range [0..100,000];
  * the elements of A are all distinct;
  * each element of array A is an integer within the range [1..(N + 1)].

_Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited._

## 풀이

```java

import java.util.*;

public class Main {
	public static void main(String[] args) {
		int[] A = {2, 3, 1, 5};
		System.out.println(solution(A));
	}
	
	public static int solution(int[] A) {
		int result = 0;
		int[] visited = new int[A.length + 2];
		
		for (int i = 0; i < A.length; i++) {
			visited[A[i]] = 1;
		}
		
		for (int i = 1; i < visited.length; i++) {
			if (visited[i] == 0) {
				result = i;
				break;
			}
		}
		
		return result;
		
		
	}
}


```
