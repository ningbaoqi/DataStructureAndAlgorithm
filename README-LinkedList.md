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

#### 两个单链表生成相加链表

```

    /**
     * 两个单链表生成相加链表
     *
     * @param head1
     * @param head2
     * @return
     */
    public Node addList2(Node head1, Node head2) {
        Stack<Integer> stack1 = new Stack<>();
        Stack<Integer> stack2 = new Stack<>();
        while (head1 != null) {
            stack1.push(head1.data);
            head1 = head1.next;
        }
        while (head2 != null) {
            stack2.push(head2.data);
            head2 = head2.next;
        }
        int n1 = 0;//链表1的数据
        int n2 = 0;//链表2的数据
        int n = 0;//n1+n2+ca
        int ca = 0;//进位
        Node node = null;//当前节点
        Node pNode = null;//当前节点的前驱节点
        while (!stack1.isEmpty() || !stack2.isEmpty()) {
            n1 = stack1.isEmpty() ? 0 : stack1.pop();
            n2 = stack2.isEmpty() ? 0 : stack2.pop();
            n = n1 + n2 + ca;
            node = new Node(n % 10);
            node.next = pNode;
            pNode = node;
            ca = n / 10;
        }
        if (ca == 1) {
            pNode = node;
            node = new Node(n / 10);
            node.next = pNode;
        }
        return node;
    }
```
#### 删除单链表中数值重复出现的节点

```
    /**
     * 删除单链表中数值重复出现的节点
     *
     * @param head
     */
    public void deleteDuplication(Node head) {
        if (head == null) {
            return;
        }
        HashSet<Integer> set = new HashSet<>();
        Node pre = head;
        Node cur = head.next;
        set.add(head.data);
        while (cur != null) {
            if (set.contains(cur.data)) {
                pre.next = cur.next;
            } else {
                set.add(cur.data);
                pre = cur;
            }
            cur = cur.next;
        }
    }
```
