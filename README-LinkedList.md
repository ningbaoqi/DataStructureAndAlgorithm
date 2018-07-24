#### 删除单链表的倒数第Ｋ个节点

```
    /**
     * 删除单链表的倒数第K个节点
     *
     * @param head
     * @param k
     * @return
     */
    public static Node removeLastKthNode(Node head, int k) {
        if (k <= 0 || head == null) {
            return head;
        }
        Node p = head;
        for (int i = 0; i < k; i++) {
            if (p.next != null) {
                p = p.next;
            } else {
                return head;
            }
        }
        Node q = head;
        while (p.next != null) {
            p = p.next;
            q = q.next;
        }
        q.next = q.next.next;
        return head;
    }
```
