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
