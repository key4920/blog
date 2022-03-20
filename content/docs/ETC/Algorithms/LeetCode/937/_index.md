+++
title = "[ LeetCode #937 ]"
date = "2022-03-20"
categories = ["Algorithms","LeetCode"]
tags = ["Algorithms" , "Python" ,"LeetCode"]
+++

# [ LeetCode #937 ] Reorder Log Files 로그 파일 재정렬

## [[ LeetCode #937 ] Reorder Log Files 바로가기 ](https://leetcode.com/problems/reorder-data-in-log-files/)

## 💡 유용한 지식

{{< hint warning >}}
**리스트 정렬**

```python
# 리스트 정렬 index 반환
index = sorted(range(len(s)), key = lambda x : s[x])
s = [s[i] for i in index]

# string split list로 sort
s.sort(key = lambda x: (x.split(' ')[1:], x.split(' ')[0]))

# 함수를 이용한 sorting
def fn(s):
	return s[0], s[-1]
sorted(a, key=fn)
sorted(a, key=len)
```

{{< /hint >}}

## 문제

You are given an array of `logs`. Each log is a space-delimited string of words, where the first word is the **identifier**.

There are two types of logs:

- **Letter-logs**: All words (except the identifier) consist of lowercase English letters.
- **Digit-logs**: All words (except the identifier) consist of digits.

Reorder these logs so that:

1. The **letter-logs** come before all **digit-logs**.
2. The **letter-logs** are sorted lexicographically by their contents. If their contents are the same, then sort them lexicographically by their identifiers.
3. The **digit-logs** maintain their relative ordering.

Return *the final order of the logs*.

{{< expand "Examples" >}}

    **Example 1:**

    ```
    Input: logs = ["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]
    Output: ["let1 art can","let3 art zero","let2 own kit dig","dig1 8 1 5 1","dig2 3 6"]
    Explanation:
    The letter-log contents are all different, so their ordering is "art can", "art zero", "own kit dig".
    The digit-logs have a relative order of "dig1 8 1 5 1", "dig2 3 6".

    ```

    **Example 2:**

    ```
    Input: logs = ["a1 9 2 3 1","g1 act car","zo4 4 7","ab1 off key dog","a8 act zoo"]
    Output: ["g1 act car","a8 act zoo","ab1 off key dog","a1 9 2 3 1","zo4 4 7"]

    ```

{{< /expand >}}

**Constraints:**

- `1 <= logs.length <= 100`
- `3 <= logs[i].length <= 100`
- All the tokens of `logs[i]` are separated by a **single** space.
- `logs[i]` is guaranteed to have an identifier and at least one word after the identifier

## 내가 했던 접근

{{< expand "실패 History" >}}

- content가 동일하면 identifiers 순으로 sorting 예외처리 안함

```python
class Solution(object):
    def reorderLogFiles(self, logs):
        letter_logs = []
        digit_logs = []
        for log in logs:
            if log.split(' ')[1].isnumeric():
                digit_logs.append(log)
            else:
                letter_logs.append(log)

        letter_logs2 = list(map(lambda x: ' '.join(x.split(' ')[1:]),letter_logs))
        sort_index = sorted(range(len(letter_logs2)) , key = lambda x: letter_logs2[x])
        letter_logs = [letter_logs[i] for i in sort_index]
        return letter_logs + digit_logs
```

{{< /expand >}}

**[ 풀이 ]**

1. log 맨 앞 identifier 다음 단어가 letter인지 digit 판별하여 각각 별도 리스트로 저장
2. letter 인 리스트 sort하면서 index 를 반환받아서 letter log 재정렬
3. 마지막 결과로 letter + digit 반환

**[ 결과 ]**

**Runtime:** 43 ms, faster than 29.75% of Python online submissions for Reorder Data in Log Files.  
**Memory Usage:** 13.8 MB, less than 23.66% of Python online submissions for Reorder Data in Log Files.

**[ 코드 ]**

```python
class Solution(object):
    def reorderLogFiles(self, logs):
        letter_logs = []
        digit_logs = []
        for log in logs:
            if log.split(' ')[1].isnumeric():
                digit_logs.append(log)
            else:
                letter_logs.append(log)

        sort_index = sorted(range(len(letter_logs)),
                            key = lambda x: (' '.join(letter_logs[x].split(' ')[1:]),
                                             letter_logs[x].split(' ')[0]))

        letter_logs = [letter_logs[i] for i in sort_index]
        return letter_logs + digit_logs
```

**[ 반성 ]**

- 굳이 index, join()해서 string으로 변환할 필요 X, list 그대로 sort 가능

```python
## 굳이 index, join()해서 string으로 변환할 필요 X, list 그대로 sort 가능하다
sort_index = sorted(range(len(letter_logs)),
                            key = lambda x: (' '.join(letter_logs[x].split(' ')[1:]),
                                             letter_logs[x].split(' ')[0]))
letter_logs = [letter_logs[i] for i in sort_index]
## 이런식으로
letter_logs.sort(key = lambda x : (x.split(' ')[1:], x.split(' ')[0]))
```

## 책 풀이

**[ 풀이 ]**

- 내 접근과 동일하지만 letter 정렬시 index가 아닌 직접 sort 함수 적용

**[ 결과 ]**

**Runtime:** 38 ms, faster than 44.80% of Python online submissions for Reorder Data in Log Files.  
**Memory Usage:** 13.7 MB, less than 77.18% of Python online submissions for Reorder Data in Log Files.

**[ 코드 ]**

```python
class Solution(object):
    def reorderLogFiles(self, logs):
        letter_logs = []
        digit_logs = []
        for log in logs:
            if log.split(' ')[1].isdigit():
                digit_logs.append(log)
            else:
                letter_logs.append(log)

        letter_logs.sort(key = lambda x : (x.split(' ')[1:], x.split(' ')[0]))
        return letter_logs + digit_logs방법 2 : Pythonic 방법, reverse() 활용
```
