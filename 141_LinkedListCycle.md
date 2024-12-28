'''
#step1
#C++

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
'''

'''
#step2
#Python

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
'''

'''
#step3
#Python
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
'''
