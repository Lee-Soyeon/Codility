# CyclicRotation

## 문제

An array A consisting of N integers is given. Rotation of the array means that each element is shifted right by one index, and the last element of the array is moved to the first place. For example, the rotation of array A = [3, 8, 9, 7, 6] is [6, 3, 8, 9, 7] (elements are shifted right by one index and 6 is moved to the first place).

The goal is to rotate array A K times; that is, each element of A will be shifted to the right K times.

Write a function:

class Solution { public int[] solution(int[] A, int K); }

that, given an array A consisting of N integers and an integer K, returns the array A rotated K times.

For example, given

    A = [3, 8, 9, 7, 6]
    K = 3
the function should return [9, 7, 6, 3, 8]. Three rotations were made:

    [3, 8, 9, 7, 6] -> [6, 3, 8, 9, 7]
    [6, 3, 8, 9, 7] -> [7, 6, 3, 8, 9]
    [7, 6, 3, 8, 9] -> [9, 7, 6, 3, 8]
For another example, given

    A = [0, 0, 0]
    K = 1
the function should return [0, 0, 0]

Given

    A = [1, 2, 3, 4]
    K = 4
the function should return [1, 2, 3, 4]

Assume that:

N and K are integers within the range [0..100];
each element of array A is an integer within the range [−1,000..1,000].
In your solution, focus on correctness. The performance of your solution will not be the focus of the assessment.

_Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited._

## 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
	public static void main(String[] args) throws NumberFormatException, IOException {
		int[] A = {3, 8, 9, 7, 6};
		int K = 3;
		int[] result = solution(A, K);
		printArray(result);
	}
	
	public static int[] solution(int[] A, int K) {
		LinkedList<Integer> queue = new LinkedList<>();
		int[] result = new int[A.length];
		
		for (int i = A.length - 1; i >= 0; i--) {
			queue.offer(A[i]);
		}
		
		for (int i = 0; i < K; i++) {
			queue.offer(queue.poll());
		}
		
		int index = A.length - 1;
		for (Integer i : queue) {
			result[index--] = i;
		}
		
		return result;
	}
	
	public static void printArray(int[] a) {
		System.out.print("[");
		for (int i = 0; i < a.length; i++) {
			if (i == a.length - 1) {
				System.out.print(a[i]);
			} else {
				System.out.print(a[i] + ", ");
			}
		}
		System.out.print("]");
	}
}
```
