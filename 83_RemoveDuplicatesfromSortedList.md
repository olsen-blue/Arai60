###83. Remove Duplicates from Sorted List

##Step1
- ノードを１つずつ見ていく解法でいけそうだなと考えた。。下記のように書いてみてAC。

```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        ptr = head

        while ptr is not None :
            if (ptr.next is not None) and (ptr.val == ptr.next.val) :
                ptr.next = ptr.next.next                    
            else :
                ptr = ptr.next
        return head
```

##Step2
- 他の人のコードも見てみる
https://github.com/ichika0615/arai60/pull/3
https://github.com/katataku/leetcode/pull/2
https://github.com/t0hsumi/leetcode/pull/3
https://github.com/pineappleYogurt/leetCode/pull/4
https://github.com/atomina1/Arai60_review/pull/2
https://github.com/SanakoMeine/leetcode/pull/4

- 再帰で解いているかたもいらっしゃったが、割とシンプルな問題なので、whileとifを使うものがしっくりきた。そう書くことにする。
- 下記の方のようにcontinueでお預けにするのが良いなと感じた。
 -【！質問！】 elseが便利で「#Step1」のようについ使ってしまうのですが、SWEの常識的にはあまり好まれないのでしょうか？ 好まれないとすると、それはelseに「例外処理」っぽい意味があるからでしょうか・・・？
https://github.com/ichika0615/arai60/pull/3

- ノードがNoneであることのチェックはまとめて書いてしまおうと思い、ついでにそのように修正にトライ。
　- 「cur.next is not None」の確認が必要なのは、cur.nextがNoneの時に、cur.next.nextにアクセスできないから。という理解です。

```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        cur = head
        while (cur is not None) and (cur.next is not None):
            if cur.val == cur.next.val :
                cur.next = cur.next.next
                continue
            cur = cur.next
        return head
```

##Step3

```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        cur = head
        while (cur is not None) and (cur.next is not None):
            if cur.val == cur.next.val :
                cur.next = cur.next.next
                continue
            cur = cur.next
        return head

```

##Step3-1
- 野田さんにいただいたアドバイスを反映
 - 「:」の前のスペースを削除
 - 略した英単語は読み手の負荷が増えるので、しない。->「cur」ではなく「node」に修正
 - 条件式を（）で囲う書き方はあまり見られないとの頃。小田さんにも同様のコメントをいただいたので修正。
```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node = head
        while node is not None and node.next is not None:
            if node.val == node.next.val:
                node.next = node.next.next
                continue
            node = node.next
        return head
```


