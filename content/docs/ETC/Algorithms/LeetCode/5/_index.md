+++
title = "[ LeetCode #5 ]"
date = "2022-03-23"
categories = ["Algorithms","LeetCode"]
tags = ["Algorithms" , "Python" ,"LeetCode"]
+++

# [ LeetCode #5 ] Longest Palindrome Substring 가장 긴 팰린드롬 부분 문자열

## [[ LeetCode #5 ] Longest Palindromic Substring 바로가기 ](https://leetcode.com/problems/longest-palindromic-substring/)

## 💡 유용한 지식

{{< hint warning >}}
**max() 함수 key 활용**

```python
max( result,
        two_pointer(i, i+1),
        two_pointer(i, i+2),
        key = len)
```

**투포인터 좁히는 방향이 아닌 확장하며 탐색**

```python
def two_pointer(left, right):
	while left >= 0 and right < len(s) and s[left] == s[right]:
		left -= 1
		right += 1
	return s[left+1:right]
```

{{< /hint >}}

---

## 문제

Given a string `s`, return *the longest palindromic substring* in `s`.

{{< expand "Examples" >}}

    **Example 1:**

    ```
    Input: s = "babad"
    Output: "bab"
    Explanation: "aba" is also a valid answer.

    ```

    **Example 2:**

    ```
    Input: s = "cbbd"
    Output: "bb"

    ```

{{< /expand >}}

**Constraints:**

- `1 <= s.length <= 1000`
- `s` consist of only digits and English letters.

---

## 내가 했던 접근

**[ 풀이(실패) ]**

- 1차 시도 : ‘가장 긴' 팰린드롬을 찾아야했기 때문에 전체 문자열부터 하나씩 길이를 줄여가며 탐색하는 방향으로 잡았다. 따라서 하나씩 길이를 줄여가면서 문자열이 팰린드롬인지 탐색했다.
- 2차 시도 : 1차 시도에 투포인터 방법을 적용해봤지만 여전히 시간초과로 실패하였다.

**[ 결과 ] Time Limit Exceed**

**[ 코드 ]**

1차 시도

```python
class Solution(object):
    def longestPalindrome(self, s):
        len_sub = 0
        while True:
            for ind in range(len_sub+1):
                new_s = s[ind:len(s)-(len_sub-ind)]
                if new_s == new_s[::-1]:
                    return new_s
            len_sub +=1
```

2차 시도

```python
class Solution(object):
    def groupAnagrams(self, strs):
        groups = dict()
        for string in strs:
            sorted_string = ''.join(sorted(string))
            if sorted_string in groups.keys():
                groups[sorted_string].append(string)
            else:
                groups[sorted_string] = [string]
        return list(groups.values())
```

**[ 반성 ]**

- 시간 복잡도가 너무 큰 방법으로, 처음에 전체 문자열부터 차츰 길이를 줄여가는 접근부터가 잘못됐다.

---

## 책 풀이

**[ 풀이 ]**

- 크게 문자열의 길이가 **짝수**인 경우 **홀수**인 경우 2가지만 존재
- 맨 앞에서부터 짝수인 경우 홀수인 경우로 나눠
  가장 짧은 길이인 2, 3일때 투포인터로 팰린드롬 판별
- 만약 팰린드롬이 맞으면 포인터를 왼쪽은 왼쪽, 오른쪽은 오른쪽으로 확장해서 가장 긴 팰린드롬을 찾는다.
- 가장 긴 팰린드롬을 저장해두고 인덱스를 넓혀가며 반복한다.

**[ 결과 ]**

**Runtime:** 809 ms, faster than 85.78% of Python online submissions for Longest Palindromic Substring.  
**Memory Usage:** 13.5 MB, less than 70.60% of Python online submissions for Longest Palindromic Substring.

**[ 코드 ]**

```python
class Solution(object):
    def longestPalindrome(self, s):
        def two_pointer(left, right):
            while left >= 0 and right < len(s) and s[left] == s[right]:
                left -= 1
                right += 1
            return s[left+1:right]

        if len(s) <= 1:
            return s

        result = ''
        for i in range(len(s)+1):
            result = max( result,
                        two_pointer(i, i+1),
                        two_pointer(i, i+2),
                        key = len)

        return result
```
