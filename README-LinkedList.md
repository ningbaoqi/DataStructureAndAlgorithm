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
#### 单链表中删除指定数值的节点

```

public class StackUtil {

    class Node {
        int data;
        Node next;

        public Node(int data) {
            this.data = data;
        }
    }

    /**
     * 单链表中删除指定数值的节点：方法一： 利用栈 : 将不等于num的值的节点利用栈，全部收集起来，收集完成之后，把全部链接起来，形成一个 新的链表
     */
    public Node removeValue1(Node head, int num) {
        Stack<Node> stack = new Stack<>();
        while (head != null) {
            if (head.data != num) {
                stack.push(head);//进栈
            }
            head = head.next;
        }
        while (!stack.isEmpty()) {//生成新的链表
            stack.peek().next = head;//获取栈顶元素，但不出栈
            head = stack.pop();//出栈
        }
        return head;
    }

    /**
     * 单链表中删除指定数值的节点方法二：不利用栈
     */
    public Node removeValue2(Node head, int num) {
        while (head != null) {//找到第一个不等于的节点，需要保留的节点，作为新链表的首节点
            if (head.data != num) {
                break;
            }
            head = head.next;
        }
        Node pre = head;
        Node cur = head;
        while (cur != null) {
            if (cur.data == num) {
                pre.next = cur.next;
            } else {
                pre = cur;
            }
            cur = cur.next;
        }
        return head;
        
    }
}

```
#### 删除单链表中的指定节点

```

public class StackUtil {

    class Node {
        int data;
        Node next;

        public Node(int data) {
            this.data = data;
        }
    }

    /**
     * 删除单链表中的指定节点
     * 根据所要删除的节点找到它后面的节点，然后将后面节点的data域赋值给当前节点的data域，同时要保证当前节点指向后面节点的后面节点，这样就能保证整个链是不断开的,实现了删除指定节点的功能
     */
    public static void deleteNode(Node head, Node node) {
        //删除尾节点，采用顺序查找找到尾节点的前一节点
        if (node.next == null) {
            while (head.next != node) {//遍历找到尾部节点
                head = head.next;
            }
            head.next = null;
        }

        //要删除的节点是头节点
        else if (head == node) {
            head = null;
        }
        //要删除的节点是中间普通节点
        else {
            Node q = node.next;
            node.data = q.data;
            node.next = q.next;
        }
    }
}

```
