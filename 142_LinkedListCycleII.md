###142. Linked List Cycle II


##Step1
- 「141.Linked List Cycle」に、＋αの続きを記載すれば良さそうであると考えた。下記コードにてAC.

#（解法１）tortise and hare
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fast = head
        slow = head

        while fast is not None and fast.next is not None :
            fast = fast.next.next
            slow = slow.next
            if fast == slow :
                fast = head
                while fast != slow :
                    fast = fast.next
                    slow = slow.next
                return fast
        return None

```

#（解法２）setを使う解法
- 「141.Linked List Cycle」のreturnで出力するものだけを変えれば良いことに気づく。
-（解法１）よりも少ない変更作業でACを出すことができた。記述量が少ないので（解法２）の方がなんとなく好きです。

```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        visited = set()
        ptr = head

        while ptr is not None :
            if ptr in visited:
                return ptr
            visited.add(ptr)
            ptr = ptr.next
        return None
```

##Step2
- 他の人のコードを見てみる
https://github.com/katataku/leetcode/pull/5/commits/9e21fbbcd282fc3051af6aa7c650927c63661846
https://github.com/t0hsumi/leetcode/pull/2/commits/bd7fa3eb9ac5ef3e272e3c786d5ae797caa9ee9f
https://github.com/pineappleYogurt/leetCode/pull/3/commits/728d06bcb738576d954602a1daf1ca3f7ae2c360
https://github.com/atomina1/Arai60_review/pull/1/commits/8fcdaa2f786ebd429c3c9d486e96c30be3173333
https://github.com/SanakoMeine/leetcode/pull/3/commits/fb29579dd112f5b183c9361e080415958bf3231e

- fastをheadに戻した後も、変数名がfastのままなのは確かに変だなと感じ、（解法１）の修正にトライした。
- (解放２)は取り急ぎこのままでも良いかもと感じた。（要修正点あればコメントください。） 


#（解法１）tortise and hare
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fast = head
        slow = head
        while (fast is not None) and (fast.next is not None) : #長いので()でくくる方が良いかもと思い、そのように修正。
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                origin = head                                   #fastではなく、originを使う
                while origin != slow :
                    origin = origin.next
                    slow   = slow.next
                return origin
        return None
```

##Step3
- Step2までの内容で最終確認にトライ

#（解法１）tortise and hare：　2分ほどでAC
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fast = head
        slow = head
        while (fast is not None) and (fast.next is not None):
            fast = fast.next.next
            slow = slow.next
            if fast == slow :
                org = head
                while org != slow :
                    org = org.next
                    slow = slow.next
                return org
        return None 
```


#（解法２）setを使う解法：　１分半ほどでAC
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        visited = set()
        ptr = head

        while ptr is not None:
            if ptr in visited :
                return ptr
            visited.add(ptr)
            ptr = ptr.next
        return None
```


