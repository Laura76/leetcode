No.146 LRU缓存机制  **LinkedHashMap(有序字典)**
```
class LRUCache extends LinkedHashMap<Integer,Integer> {
    private int capacity;

    public LRUCache(int capacity) {
        super(capacity,0.75f,true);
        this.capacity=capacity;
    }

    public int get(int key) {
        return super.getOrDefault(key,-1);
    }

    public void put(int key, int value) {
        super.put(key,value);
    }
    @Override
    protected boolean removeEldestEntry(Map.Entry<Integer,Integer> eldest){
        return this.size()>this.capacity;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```
No.147 对链表进行插入排序  **让链表远离我**  
No.148 排序链表  **走开啊链表**  
No.149 直线上最多的点数  **困难模式**  
No.150 逆波兰表达式求值  **栈**
```
import java.util.regex.Pattern;
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack=new Stack<Integer>();
        for(String str:tokens){
            Pattern pattern = Pattern.compile("^[-\\+]?[\\d]+$");  
            if(pattern.matcher(str).matches()){
                stack.push(Integer.parseInt(str));    
            }else{
                int after=stack.pop();
                int before=stack.pop();
                switch(str){
                    case "+":
                        stack.push(before+after);break;
                    case "-":
                        stack.push(before-after);break;
                    case "*":
                        stack.push(before*after);break;
                    case "/":
                        stack.push(before/after);break;
                    default:break;
                }
            }
        }
        return stack.pop();
    }
}
```
