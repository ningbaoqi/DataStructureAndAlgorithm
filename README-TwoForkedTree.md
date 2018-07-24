#### 后续遍历
```
/**
 * 后序遍历：迭代
 *
 * @param root
 */
public static void postorderTraversal(TreeNode root) {
    if (root == null) {
        return;
    }
    Stack<TreeNode> s = new Stack<>();//第一个stack用于添加node和它的左右孩子
    Stack<TreeNode> output = new Stack<>();//第二个stack用于翻转第一个stack输出
    s.push(root);
    while (!s.isEmpty()) {//确保所有元素都被翻转转移到第二个stack
        TreeNode cur = s.pop();//把栈顶元素添加到第二个stack
        output.push(cur);
        if (cur.left != null) {//把栈顶元素的左孩子和右孩子分别添加到第一个stack
            s.push(cur.left);
        }
        if (cur.right != null) {
            s.push(cur.right);
        }
        while (!output.isEmpty()) {
            //遍历输出第二个stack，即为后续遍历
        }
    }
}
```
#### 中序遍历

```
    /**
     * 中序遍历：递归
     *
     * @param root
     */
    public static void inorderTraversalRec(TreeNode root) {
        if (root == null) {
            return;
        }
        inorderTraversalRec(root.left);
        inorderTraversalRec(root.right);
    }

    /**
     * 中序遍历：迭代
     *
     * @param root
     */
    public static void inorderTraversal(TreeNode root) {
        if (root == null) {
            return;
        }
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        if (cur != null) {
            while (!stack.isEmpty() || cur != null) {
                if (cur != null) {
                    stack.push(cur);
                    cur = cur.left;
                } else {
                    cur = stack.pop();
                    cur = cur.right;
                }
            }
        }
    }
```
#### 前序遍历二叉树
```
    /**
     * 前序遍历：递归
     *
     * @param root
     */
    public static void preorderTraversalRec(TreeNode root) {
        if (root == null) {
            return;
        }
        preorderTraversalRec(root.left);
        preorderTraversalRec(root.right);
    }
```

```
    /**
     * 前序遍历 迭代
     *
     * @param root
     */
    public static void preorderTraversal(TreeNode root) {
        if (root == null) {
            return;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode cur = stack.pop();//出栈栈顶元素
            if (cur.right != null) {//关键点：要先压入右孩子，再压入左孩子，这样在出栈时会先打印左孩子再打印右孩子
                stack.push(cur.right);
            }
            if (cur.left != null) {
                stack.push(cur.left);
            }
        }
    }
```

#### 分层遍历二叉树
```
    /**
     * 分层遍历二叉树迭代，（宽度优先遍历)
     *
     * @param root
     */
    public static void levelTraversal(TreeNode root) {
        if (root == null) {
            return;
        }
        LinkedList<TreeNode> quequ = new LinkedList<>();
        quequ.push(root);
        while (!quequ.isEmpty()) {
            TreeNode cur = quequ.removeFirst();
            if (cur.left != null) {
                quequ.add(cur.left);
            }
            if (cur.right != null) {
                quequ.add(cur.right);
            }
        }
    }
```
##### 分层遍历应用：按层打印二叉树
```
    /**
     * 分层遍历应用：按层打印二叉树
     *
     * @param root
     * @return
     */
    public ArrayList<Integer> printFromTopToBottom(TreeNode root) {
        ArrayList<Integer> list = new ArrayList<>();
        Queue<TreeNode> queue = new ArrayBlockingQueue<TreeNode>(100);
        TreeNode last = root;//当前行的最右节点
        TreeNode nLast = root;//下一行的最右节点
        queue.add(root);
        while (!queue.isEmpty()) {
            TreeNode out = queue.poll();
            list.add(out.val);
            if (out.left != null) {
                queue.add(out.left);
                nLast = out.left;
            }
            if (out.right != null) {
                queue.add(out.right);
                nLast = out.right;
            }
            if (out == last) {
                last = nLast;
            }
        }
        return list;
    }
```
