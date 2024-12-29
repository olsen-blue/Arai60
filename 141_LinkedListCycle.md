###141_LinkedListCycle：tortise and hare

##Step1
#思考メモ
- 初見では全く分からなかったのでAraiさんの動画を参照して、slowとfastの2ポインタの解法を知り、まずこれを理解して書いてみました。
```cpp

class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (!head || !head->next) return false; // 空のリストまたは1つの要素しかない場合、サイクルはない

        ListNode *slow = head; // スローポインタ
        ListNode *fast = head; // ファストポインタ

        while (fast && fast->next) {
            slow = slow->next;            // スローポインタは1ステップ進む
            fast = fast->next->next;      // ファストポインタは2ステップ進む

            if (slow == fast) return true; // スローポインタとファストポインタが交差した場合、サイクルが存在
        }

        return false; // ファストポインタがnullに到達した場合、サイクルは存在しない
    }
};
```

##Step2
#思考メモ
- Pythonの方が文字数少なく簡潔に書けそうだなと思い、Pythonにチェンジ。すっきりとした見た目になり、その点では満足した。
```python

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        slow = head
        fast = head
        while fast != None and fast.next != None:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```

##Step3
#思考メモ
- slowとfastの2ポインタの解法が頭に染み込んできたので、step3にトライ。2分くらいで書けるようになっていました。
```python
class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        slow = head
        fast = head
        while fast != None and fast.next != None:
            slow = slow.next
            fast = fast.next.next
            if slow == fast :
                return True
        return False
```

##Step4
#思考メモ
- 小田さんにPython3の方が最近は主流だと聞いたので、Python3で書いてみる。引数と関数出力を明示的に書くことができるのが良いなと感じた。Python3で今後は行きたいと思います。
- Pythonでは「!= None」ではなく「not」を用いて「is not None」とする方が一般的らしいことを知る。
```python3
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:   #Optional[ListNode]は、ListNode(ノードがないときはNone）型になることを示している。fast
        fast = head
        slow = head
        while fast is not None and fast.next is not None :
            fast = fast.next.next
            slow = slow.next
            if fast == slow :
                return True
        return False 

```

###141_LinkedListCycle：setを使う解法

##Step1
#思考メモ
-小田さんに他の人のコードも見た方が良い、とアドバイスいただいたので、レビュー依頼のチャンネルを見てみる。
- 下記のようにsetを使う解法もあるということが判明。
- https://github.com/SanakoMeine/leetcode/pull/2/commits/dc7882e988cfdca0b90f0ddfdc0f2fbc06fd0e83
- https://github.com/lilnoahhh/leetcode/pull/1/commits/b801f023a2bdb72b034187c582c2eabb57af4322
- https://github.com/t0hsumi/leetcode/pull/1/commits/ce258d2ca2d5cdbd432c861934ce4cf0660fff40
- https://github.com/onyx0831/leetcode/pull/1/commits/b71dec85200961235b3941ebd2fe9a7f88074669
- https://github.com/katataku/leetcode/pull/1/commits/66c304778c45cf881d127be78d209f4d8ea036bb

- 下記の問題と似た考え方だなと理解・納得しました。（->本Discordサーバーに参加する前にLeetCodeの問を題いくつか解くことを個人でしておりました。）
- https://leetcode.com/problems/two-sum/description/
- https://leetcode.com/problems/intersection-of-two-arrays/description/
- https://leetcode.com/problems/subarray-sum-equals-k/description/

-真似して書いてみる。下記でACとなりました。
```python3
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:   #Optional[ListNode]は、ListNode(ノードがないときはNone）型になることを示している。fast
        visited = set() #空集合を作る
        ptr = head

        while ptr :
            if ptr in visited :
                return True
            visited.add(ptr)      #集合への追加はadd。リストへの追加はappend。
            ptr = ptr.next
        return False
```
##Step2
- 「while ptr」のところは「while ptr is not None」の方が明示的ではと思い、そのように修正。

```python3
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:   #Optional[ListNode]は、ListNode(ノードがないときはNone）型になることを示している。fast
        visited = set ()
        ptr = head

        while ptr is not None:
            if ptr in visited :
                return True
            visited.add(ptr)
            ptr = ptr.next
        
        return False
```

##Step3
```python3
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:   #Optional[ListNode]は、ListNode(ノードがないときはNone）型になることを示している。fast
        visited = set()
        ptr = head

        while ptr is not None :
            if ptr in visited :
                return True
            visited.add(ptr)
            ptr = ptr.next

        return False 
```
