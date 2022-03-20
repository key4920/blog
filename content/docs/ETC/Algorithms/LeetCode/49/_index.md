+++
title = "[ LeetCode #49 ]"
date = "2022-03-20"
categories = ["Algorithms","LeetCode"]
tags = ["Algorithms" , "Python" ,"LeetCode"]
+++

# [ LeetCode #49 ] Group Anagrams 그룹 애너그램

## [[ LeetCode #49 ] Group Anagrams 바로가기 ](https://leetcode.com/problems/group-anagrams/)

## 💡 유용한 지식

{{< hint warning >}}
**Dictionary defaultdict 객체**

- 존재하지 않는 키를 조회할 경우 에러 메시지 대신 디폴트 값을 기준으로 키에 대한 딕셔너리 아이템을 생성해줌

```python
# defaultdict() 사용으로 불필요한 if 연산 제거
from collections import defaultdict
groups = defaultdict(list)
```

{{< /hint >}}

---

## 문제

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

{{< expand "Examples" >}}

    **Example 1:**

    ```
    Input: strs = ["eat","tea","tan","ate","nat","bat"]
    Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
    ```

    **Example 2:**

    ```
    Input: strs = [""]
    Output: [[""]]
    ```

    **Example 3:**

    ```
    Input: strs = ["a"]
    Output: [["a"]]
    ```

{{< /expand >}}

**Constraints:**

- `1 <= strs.length <= 104`
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lowercase English letters.

---

## 내가 했던 접근

{{< expand "실패 History" >}}
{{< /expand >}}

**[ 풀이 ]**

- input 단어를 각각 sorted() 후 동일한 단어끼리 딕셔너리로 그룹을 묶고 values() 로 결과 반환

**[ 결과 ]**

**Runtime:** 1956 ms, faster than 7.46% of Python online submissions for Group Anagrams.  
**Memory Usage:** 17.3 MB, less than 83.24% of Python online submissions for Group Anagrams.

**[ 코드 ]**

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

- dict() 대신 collections.defaultdict(list) 사용하면 불필요한 if문 제거 가능

---

## 책 풀이

**[ 풀이 ]**

- 내 접근과 동일하지만 dict() 대신 collections.defaultdict(list) 사용하여 불필요한 if문 제거 가능

**[ 결과 ]**

**Runtime:** 117 ms, faster than 58.08% of Python online submissions for Group Anagrams.  
**Memory Usage:** 17.6 MB, less than 71.25% of Python online submissions for Group Anagrams.

**[ 코드 ]**

```python
from collections import defaultdict
class Solution(object):
    def groupAnagrams(self, strs):
        groups = defaultdict(list)
        for string in strs:
            groups[''.join(sorted(string))].append(string)
        return list(groups.values())
```
