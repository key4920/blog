+++
title = "[ LeetCode #1 ]"
date = "2022-03-23"
categories = ["Algorithms","LeetCode"]
tags = ["Algorithms" , "Python" ,"LeetCode"]
+++

# [ LeetCode #1 ] Two Sum 두 수의 합

## [[ LeetCode #1 ] Two Sum 바로가기 ](https://leetcode.com/problems/two-sum/)

## 💡 유용한 지식

{{< hint warning >}}

**index() 함수 start, end 인자**

```python
## index()함수 인자
# - start, end ; (optional)조회하려는 리스트 시작과 끝 인덱스
index(value, start, end)
```

**Dictionary 의 조회는 O(1)**

- 키/값 구조로 이루어져 있으며 입력 순서가 유지(버전 3.7이상)되며 내부적으로는 해시 테이블로 구현되어 있다.
- 다양한 타입을 키로 지원하면서도 입력과 조회 모두 분할 상환 분석에 따른 시간 복잡도는 O(1)로 가능하다.(최악의 경우엔 O(n))
  | 연산 | 시간 복잡도 |
  | --- | --- |
  | len(a) | O(1) |
  | a[key] | O(1) |
  | a[key] = value | O(1) |
  | key in a | O(1) |

{{< /hint >}}

---

## 문제

Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

{{< expand "Examples" >}}
**Example 1:**

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```
Input: nums = [3,2,4], target = 6
Output: [1,2]

```

**Example 3:**

```
Input: nums = [3,3], target = 6
Output: [0,1]

```

{{< /expand >}}

**Constraints:**

- `2 <= nums.length <= 104`
- `109 <= nums[i] <= 109`
- `109 <= target <= 109`
- **Only one valid answer exists.**

**Follow-up:**

Can you come up with an algorithm that is less than O(n^2) time complexity?

---

## 내가 했던 접근

**[ 풀이 ]**

- num 앞에서부터 읽으면서 target - num 이 num의 index 뒤에 있는지 판별 후 있으면 리턴

**[ 결과 ]**

**Runtime:** 573 ms, faster than 49.33% of Python online submissions for Two Sum.
**Memory Usage:** 14.1 MB, less than 87.35% of Python online submissions for Two Sum.

**[ 코드 ]**

```python
class Solution(object):
    def twoSum(self, nums, target):
        for ind, num in enumerate(nums):
            sub_target = target - num
            if sub_target in nums[ind+1:]:
                sub_ind = nums.index(sub_target, ind+1, len(nums))
                return [ind, sub_ind]
```

**[ 반성 ]**

- 복잡도 O(n^2) 인 것 같다. 더 나은 방법 있을 것 같다.

---

## 책 풀이

**[ 풀이 ]**

- 방법 1 : 부르트포스
  - 이중 for 문으로 앞에서부터 전체 탐색
  - 복잡도 O(n^2)
- 방법 2 : in 활용 ( 내 접근과 유사 )
  - 방법 1과 동일하지만 in 활용
  - 복잡도 O(n^2) 로 동일하지만 훨씬 빠르다.
- **방법 3 : 딕셔너리 활용 \*\***
  - 딕셔너리의 조회가 O(1)인 점을 이용하여 dictionary에 값의 index를 저장해두면서 target - num을 조회
- 만약 정렬된 리스트라면 투포인터 방법도 좋았겠지만, 정렬에도 시간이 쓰이고 문제가 인덱스 반환이라 불가능했다.

**[ 결과 ]**

방법 1 : 브루트포스 (5294 ms)

**Runtime:** 5294 ms, faster than 12.44% of Python online submissions for Two Sum.
**Memory Usage:** 14.4 MB, less than 46.22% of Python online submissions for Two Sum.

방법 2 : in 활용(내 접근과 유사) (463 ms)

**Runtime:** 463 ms, faster than 52.12% of Python online submissions for Two Sum.
**Memory Usage:** 13.9 MB, less than 97.93% of Python online submissions for Two Sum.

방법 3 : 딕셔너리 활용 (36ms) \*\*

**Runtime:** 36 ms, faster than 99.52% of Python online submissions for Two Sum.
**Memory Usage:** 13.9 MB, less than 99.01% of Python online submissions for Two Sum.

**[ 코드 ]**

방법 1 : 브루트포스 (5294 ms)

```python
class Solution(object):
    def twoSum(self, nums, target):
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
```

방법 2 : in 활용(내 접근과 유사) (463 ms)

```python
class Solution(object):
    def twoSum(self, nums, target):
        for i, num in enumerate(nums):
            sub_target = target - num
            if sub_target in nums[i+1:]:
                return [nums.index(num) , nums[i+1:].index(sub_target)+(i+1)]

## 내 풀이와 다른 점 : index() 찾는법
# 내 방법 : index()함수에서 start, end 활용
nums.index(sub_target, ind+1, len(nums))
# 책 풀이 : 이전 탐색 index 이후 리스트에서 찾기
nums[i+1:].index(sub_target)+(i+1)
```

방법 3 : 딕셔너리 활용 (36ms) \*\*

```python
class Solution(object):
    def twoSum(self, nums, target):
        index_dict = dict()
        for i, num in enumerate(nums):
            sub_target = target - num
            if sub_target in index_dict:
                return [index_dict[sub_target], i]
            index_dict[num] = i
```
