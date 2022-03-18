+++
title = "[ LeetCode #344 ]"
date = "2022-03-18"
categories = ["Algorithms","LeetCode"]
tags = ["Algorithms" , "Python" ,"LeetCode"]
+++

# [ LeetCode #344 ] Reverse String 문자열 뒤집기

## [[ LeetCode #344 ] Reverse String 바로가기 ](https://leetcode.com/problems/reverse-string/)

## 💡 유용한 지식

{{< hint warning >}}
**리스트 역순으로 정렬**

```python
# reverse() 함수 활용
s.reverse()

# 슬라이싱 방법 활용
s = s[::-1]
s[:] = s[::-1]

# 투포인터를 활용하는 방법도 있다.
def reverseString(s):
	left, right = 0, len(s)-1
	while left < right:
		s[left], s[right] = s[right], s[left]
		left += 1
		right -= 1
	return s
```

{{< /hint >}}

## 문제

Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with `O(1)` extra memory.

{{< expand "Examples" >}}
**Example 1:**

```
Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]

```

**Example 2:**

```
Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]

```

{{< /expand >}}

**Constraints:**

- `1 <= s.length <= 105`
- `s[i]` is a [printable ascii character](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

## 내가 했던 접근

{{< expand "실패 History" >}}

- 슬라이싱을 활용하여 s[::-1] 만으로 제출하려했지만 O(1) 의 메모리 공간만 허용해서 불가능했다.

{{< /expand >}}

**[ 풀이 ]**

메모리 공간이 O(1) 만 있으므로 끝에서부터 pop()하여 맨 앞에 insert() 수행

**[ 결과 ]**

**Runtime:** 628 ms, faster than 5.01% of Python online submissions for Reverse String.  
**Memory Usage:** 22 MB, less than 7.54% of Python online submissions for Reverse String.

**[ 코드 ]**

```python
class Solution(object):
    def reverseString(self, s):
        for i in range(len(s)-1):
            s.insert(i, s.pop())
        return s

## 초기 생각 : 슬라이싱 s[::-1]
```

**[ 반성 ]**

- 처음에는 슬라이싱으로 해결하려했지만 extra memory O(1)을 간과했다. 따라서 insert로 접근
- 새로 리스트 만드는건 물론 더 메모리를 잡아먹으므로 불가능
- 메모리에만 집중해서 시간복잡도는 생각을 못했다.

## 책 풀이

**[ 풀이 ]**

- 총 3가지 방법 소개
  - 방법 1 : 투포인터
  - 방법 2 : Pythonic 방법, reverse() 활용
  - 방법 3 : Pythonic 방법, 슬라이싱 활용

**[ 결과 ]**

방법 1 : 투포인터

**Runtime:** 215 ms, faster than 55.01% of Python online submissions for Reverse String.  
**Memory Usage:** 21 MB, less than 81.03% of Python online submissions for Reverse String.

방법 2 : Pythonic 방법, reverse() 활용

**Runtime:** 162 ms, faster than 95.45% of Python online submissions for Reverse String.  
**Memory Usage:** 21.3 MB, less than 29.73% of Python online submissions for Reverse String.

방법 3 : Pythonic 방법, 슬라이싱 활용

**Runtime:** 164 ms, faster than 95.03% of Python online submissions for Reverse String.  
**Memory Usage:** 20.9 MB, less than 94.74% of Python online submissions for Reverse String.

**[ 코드 ]**

방법 1 : 투포인터

```python
class Solution(object):
    def reverseString(self, s):
        left, right = 0, len(s)-1
        while left < right:
            s[left],s[right] = s[right], s[left]
            left += 1
            right -= 1
        return s
```

방법 2 : Pythonic 방법, reverse() 활용

```python
class Solution(object):
    def reverseString(self, s):
        s.reverse()
        return s
```

방법 3 : Pythonic 방법, 슬라이싱 활용

```python
class Solution(object):
    def reverseString(self, s):
        s[:] = s[::-1]
        return s
# s = s[::-1] 을 사용하면 메모리가 부족하지만
# s[:] = s[::-1] 을 사용하면 된다.
```
