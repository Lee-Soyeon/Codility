# BinaryGap

## 문제

A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

  * class Solution { public int solution(int N); }

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an efficient algorithm for the following assumptions:

  * N is an integer within the range [1..2,147,483,647].
  
Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

## 풀이

``` java
import java.io.*;

public class Main {
	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine());
		System.out.println(solution(N));
	}
	
	public static int solution(int N) {
		String binary = Integer.toBinaryString(N);
		String[] s = binary.split("1");
		int max = 0, length = s.length;
		
		if (binary.charAt(binary.length() - 1) != '1') {
			length--;
		}
		
		for (int i = 0; i < length; i++) {
			if (max < s[i].length()) {
				max = s[i].length();
			}
		}
		
        return max;
	}
}
```

## 문제 해결 방법

* N을 String으로 변환함
* 1을 기준으로 문자열을 나눠 배열에 담음
* 만약, 마지막 숫자가 '1'이 아니라면 배열의 마지막 인덱스는 고려하지 않음
* 배열을 돌면서 가장 '0'의 길이가 긴 값을 
