+++
title = "[ LeetCode #819 ]"
date = "2022-03-20"
categories = ["Algorithms","LeetCode"]
tags = ["Algorithms" , "Python" ,"LeetCode"]
+++

# [ LeetCode #819 ] Most Common Word 가장 흔한 단어

## [[ LeetCode #819 ] Most Common Word 바로가기 ](https://leetcode.com/problems/most-common-word/)

## 💡 유용한 지식

{{< hint warning >}}
**Dictionary TIPS!**

```python
# 빈도 세기
from collections import Counter
count_dict = Counter(re.sub('[^a-z0-9]',' ',paragraph.lower()).split())

# key 삭제
for word in banned:
	del count_dict[word]

# 가장 높은 빈도 추출 : most_common()
# - (0)이 아닌 (1) 이 가장 높은 빈도
# - return = (key,value)
count_dict.most_common(1)[0][0]

# defaultdict() 사용으로 불필요한 if 연산 제거
from collections import defaultdict
groups = defaultdict(list)
```

{{< /hint >}}

## 문제

Given a string `paragraph` and a string array of the banned words `banned`, return *the most frequent word that is not banned*. It is **guaranteed** there is **at least one word** that is not banned, and that the answer is **unique**.

The words in `paragraph` are **case-insensitive** and the answer should be returned in **lowercase**.

{{< expand "Examples" >}}
**Example 1:**

```
Input: paragraph = "Bob hit a ball, the hit BALL flew far after it was hit.", banned = ["hit"]
Output: "ball"
Explanation:
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph.
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"),
and that "hit" isn't the answer even though it occurs more because it is banned.

```

**Example 2:**

```
Input: paragraph = "a.", banned = []
Output: "a"
```

{{< /expand >}}

**Constraints:**

- `1 <= paragraph.length <= 1000`
- paragraph consists of English letters, space `' '`, or one of the symbols: `"!?',;."`.
- `0 <= banned.length <= 100`
- `1 <= banned[i].length <= 10`
- `banned[i]` consists of only lowercase English letters.

## 내가 했던 접근

{{< expand "실패 History" >}}
{{< /expand >}}

**[ 풀이 ]**

1. input 읽으면서 클렌징하고 Counter() 함수로 단어별 빈도 딕셔너리 생성
2. banned 리스트 읽으면서 딕셔너리에서 key 삭제
3. 딕셔너리의 most_common() 함수 활용하여 결과 반환

**[ 결과 ]**

**Runtime:** 32 ms, faster than 65.55% of Python online submissions for Most Common Word.  
**Memory Usage:** 13.7 MB, less than 39.48% of Python online submissions for Most Common Word.

**[ 코드 ]**

```python
from collections import Counter
import re
class Solution(object):
    def mostCommonWord(self, paragraph, banned):
        count_dict = Counter(re.sub('[^a-z0-9]',' ',paragraph.lower()).split())
        for word in banned:
            del count_dict[word]
        return count_dict.most_common(1)[0][0]
```

**[ 반성 ]**

- Counter 딕셔너리를 모두 생성 후 banned 리스트 단어를 삭제하는데
  클렌징 과정에서 banned 리스트 단어를 삭제하면서 Counter 딕셔너리 생성 가능

## 책 풀이

**[ 풀이 ]**

- 내 접근과 동일하지만 input 클렌징시 banned 단어 삭제

**[ 결과 ]**

**Runtime:** 39 ms, faster than 45.79% of Python online submissions for Most Common Word.  
**Memory Usage:** 13.6 MB, less than 66.92% of Python online submissions for Most Common Word.

**[ 코드 ]**

```python
from collections import Counter
import re
class Solution(object):
    def mostCommonWord(self, paragraph, banned):
        words = [word for word in re.sub('[^\w]',' ',paragraph.lower()).split() if word not in banned]

        count_dict = Counter(words)
        return count_dict.most_common(1)[0][0]
```
