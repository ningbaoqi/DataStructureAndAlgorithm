#### 设计栈
```
/**
 * 设计含最小函数min()的栈，要求min push pop 的时间复杂度都是0(1)，min方法的作用是：就能返回栈中的最小值
 */
public class MinStack {
    Stack<Integer> stack = new Stack<>();//定义用来存储数据的栈
    Stack<Integer> minStack = new Stack<>();//定义用来存放最小数据的栈

    /***
     * 添加数据，首先是往stack栈中添加
     * 如果最小minStack为空，或者栈顶的元素比新添加的元素要大，则将新元素也要添加到辅助栈中
     * @param node
     */
    public void push(int node) {
        stack.push(node);
        if (minStack.isEmpty() || ((int) minStack.peek() >= node)) {
            minStack.push(node);
        }
    }

    /**
     * 如偶stack为空，直接返回
     * 如果stack不为空，得到栈顶元素，同时将栈顶元素弹出
     * 如果最小栈的栈顶元素与stack弹出的元素相等，那么最小栈也要将其弹出
     */
    public void pop() {
        if (stack.isEmpty()) {
            return;
        }
        int node = stack.peek();
        stack.pop();
        if (minStack.peek() == node) {
            minStack.pop();
        }
    }

    /**
     * 查看栈的最小元素
     *
     * @return
     */
    public int min() {
        return minStack.peek();//返回栈顶元素，不弹出
    }
}
```
#### 通过两个栈实现一个队列
+ `栈先进后出，队列先进先出`；
```
/**
 * 通过两个栈实现一个队列
 */
public class QueueWithStack {
    private static Stack<Object> stack1 = new Stack<>();//用于压入数据
    private static Stack<Object> stack2 = new Stack<>();//用于弹出数据

    /**
     * 加入队列中的元素只加入到栈1中
     */
    public static void appentTail(Object item) {
        stack1.push(item);
    }

    /**
     * 删除一个元素时，检查栈2是否为空，栈2不为空则弹出栈2栈顶元素，栈2为空，则把栈1中的元素全部弹出、压入到栈2中，然后从栈2栈顶弹出元素
     */
    public static void deleteHead() {
        if (!stack2.empty()) {
            stack2.pop();
        } else {
            if (stack1.empty()) {
                throw new RuntimeException("队列为空");
            }
            while (!stack1.empty()) {
                Object item = stack1.pop();
                stack2.push(item);
            }
        }
    }
}
```
