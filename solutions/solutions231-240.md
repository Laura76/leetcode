- No.231 2的幂  **循环除以二**
```
class Solution {
    public boolean isPowerOfTwo(int n) {
        if(n==0)return false;
        if(n==1)return true;
        while(n%2==0)n=n/2;
        if(n!=1)return false;
        else return true;
    }
}
```
- No.232 用栈实现队列  **辅助栈**
```
class MyQueue {
    private Stack<Integer> stack;
    private Stack<Integer> helpStack;
    /** Initialize your data structure here. */
    public MyQueue() {
        stack=new Stack<Integer>();
        helpStack=new Stack<Integer>();
    }

    /** Push element x to the back of queue. */
    public void push(int x) {
        while(!stack.isEmpty())helpStack.push(stack.pop());
        stack.push(x);
        while(!helpStack.isEmpty())stack.push(helpStack.pop());
    }

    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        return stack.pop();
    }

    /** Get the front element. */
    public int peek() {
        return stack.peek();
    }

    /** Returns whether the queue is empty. */
    public boolean empty() {
        return stack==null||stack.isEmpty();
    }
}
/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```
