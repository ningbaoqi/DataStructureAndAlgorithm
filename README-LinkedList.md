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
#### 判断一个单链表是否为回文结构

```  
    /**
     * 判断一个单链表是否为回文结构，回文结构：如果按次序1 2 3 4 反转之后 4 3 2 1 这就不是回文结构；如果是 1 2 2 1 反过来 1 2 2 1 正序和反序一样就是回文结构
     *
     * @param head
     * @return
     */
    public boolean isPalindrome1(Node head) {
        if (head == null) {
            return false;
        }
        Stack<Node> stack = new Stack<>();
        Node cur = head;
        while (cur != null) {//记住这个地方不是cur.next不然最后一个节点没有压入栈
            stack.push(cur);
            cur = cur.next;
        }
        while (head.next != null) {
            if (head.data != stack.pop().data) {
                return false;
            }
            head = head.next;
        }
        return true;
    }
```

