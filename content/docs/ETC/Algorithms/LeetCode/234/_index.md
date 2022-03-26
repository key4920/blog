+++
title = "[ LeetCode #234 ]"
date = "2022-03-26"
categories = ["Algorithms","LeetCode"]
tags = ["Algorithms" , "Python" ,"LeetCode"]
+++

# [ LeetCode #234 ] Palindrome Linked List 팰린드롬 연결 리스트

## [[ LeetCode #234 ] Palindrome Linked List 바로가기 ](https://leetcode.com/problems/palindrome-linked-list/)

## 💡 유용한 지식

{{< hint warning >}}

**러너 기법**

- 연결 리스트를 순회할 때 2개의 포인터를 동시에 사용하는 기법
- 빠른 러너와 느린 러너를 생성하여 병합 지점이나 중간 위치, 길이 등을 판별할 때 유용
- 빠른 러너가 연결 리스트의 끝에 도달하면 느린 러너는 연결 리스트의 중간 지점을 가리키게 되어 중간 위치를 찾아내면 값 비교하거나 뒤집기를 시도하는 등 다각도로 활용이 가능

```python
## runner 기법
# - fast, slow 는 모두 Linked List
# - fast 에 값이 있다면 길이가 홀수인 경우이므로 한칸 더 전진시킨다.
while fast and fast.next:
	fast = fast.next.next
	history, history.next, slow = slow, history, slow.next
if fast:
	slow = slow.next
```

**다중 할당 (Multiple Assignment)**

- 파이썬은 원시 타입이 존재하지 않고 모든 것이 객체
- 줄을 구분해서 할당하면 [history](http://history.next) = slow 구문으로 인해 같은 객체를 참조를 할당하므로 줄을 나누는 것과 한번에 처리하는 것은 다른 풀이가 된다.

```python
history, history.next, slow = slow, history, slow.next
```

{{< /hint >}}

---

## 문제

Given the `head` of a singly linked list, return `true` if it is a palindrome.

{{< expand "Examples" >}}
**Example 1:**
![https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
Input: head = [1,2,2,1]
Output: true

```

**Example 2:**
![https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

```
Input: head = [1,2]
Output: false

```

{{< /expand >}}

**Constraints:**

- The number of nodes in the list is in the range `[1, 105]`.
- `0 <= Node.val <= 9`

**Follow up:**

Could you do it in O(n) time and O(1) space?

---

## 내가 했던 접근

{{< expand "실패 History" >}}

- linked list 개념을 잘 이해하지 못했으며 palindrome 판별이라는 것을 잊고 조금 헤맸다.
  {{< /expand >}}

**[ 풀이 ]**

- 리스트에 append 후 슬라이싱으로 판별하기

**[ 결과 ]**

**Runtime:** 1214 ms, faster than 68.41% of Python online submissions for Palindrome Linked List.
**Memory Usage:** 85.6 MB, less than 17.58% of Python online submissions for Palindrome Linked List.

**[ 코드 ]**

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def isPalindrome(self, head):
        history = list()
        if head.next is None:
            return True

        while head:
            history.append( head.val )
            head = head.next

        return history == history[::-1]
```

**[ 반성 ]**

- linked list 특성을 살리지 못한 풀이

---

## 책 풀이

**[ 풀이 ]**

- 방법 1 : list + pop(0) (내 접근과 유사)
  - 나는 팰린드롬 판별을 리스트 슬라이싱으로 했지만 pop(0)을 사용
- 방법 2 : deque + popleft()
  - 방법 1 은 pop(0) 으로 조회가 O(n)이었지만 데크 자료형으로 O(1)로 조회 가능
- **방법 3 : 러너 \*\***
  - fast, slow 러너 2가지를 만들고 fast는 두칸씩, slow는 한칸씩 전진시켜 fast가 끝에 도달할때 slow를 중간지점에 위치시킨다.
  - slow가 오면서 지나친 길을 역순으로 history를 만들고 만약 길이가 홀수였으면 slow 를 한칸 더 전진 시킨다.
  - slow의 중간을 지나친 값과 역순으로 기록해둔 history의 값을 차례로 비교한다.
  - 모두 일치하여 slow가 None이 되면 True, 아니면 False 반환

**[ 결과 ]**

방법 1 : list + pop(0) (내 접근과 유사)

**Runtime:** 1690 ms, faster than 23.68% of Python online submissions for Palindrome Linked List.

**Memory Usage:** 84.7 MB, less than 46.59% of Python online submissions for Palindrome Linked List.

방법 2 : deque + popleft()

Runtime: 1469 ms, faster than 41.47% of Python online submissions for Palindrome Linked List.
Memory Usage: 84.5 MB, less than 51.87% of Python online submissions for Palindrome Linked List.

**방법 3 : (연결리스트 특성 활용한 방법) 러너 (992 ms)\*\***

**Runtime:** 992 ms, faster than 93.93% of Python online submissions for Palindrome Linked List.

**Memory Usage:** 49.6 MB, less than 96.18% of Python online submissions for Palindrome Linked List.

**[ 코드 ]**

방법 1 : list + pop(0) (1690 ms)

```python
class Solution(object):
    def isPalindrome(self, head):
        history = list()

        if head.next is None:
            return True

        while head:
            history.append( head.val )
            head = head.next

        while len(history) > 1 :
            if history.pop(0) != history.pop():
                return False

        return True
```

방법 2 : deque + popleft() (1469 ms)

```python
from collections import deque
class Solution(object):
    def isPalindrome(self, head):
        history = deque()

        if head.next is None:
            return True

        while head:
            history.append( head.val )
            head = head.next

        while len(history) > 1 :
            if history.popleft() != history.pop():
                return False
        return True
```

**방법 3 : (연결리스트 특성 활용한 방법) 러너 (992 ms)\*\***

```python
class Solution(object):
    def isPalindrome(self, head):

        history = None
        fast = slow = head

        while fast and fast.next:
            fast = fast.next.next
            history, history.next, slow = slow, history, slow.next
        if fast:
            slow = slow.next

        while history and history.val == slow.val:
            history, slow = history.next, slow.next
        return not slow
```
