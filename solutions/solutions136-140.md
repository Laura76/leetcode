- No.136 只出现一次的数字 **数学**
```
class Solution {
    public int singleNumber(int[] nums) {
        int res=0;
        for(int i:nums){
            res^=i;
        }
        return res;
    }
}
```
- No.137 只出现一次的数字 II  **map**
```
class Solution {
    public int singleNumber(int[] nums) {
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i:nums){
            map.put(i,map.getOrDefault(i,0)+1);
        }
        Iterator<Map.Entry<Integer, Integer>> entries = map.entrySet().iterator();
        while(entries.hasNext()){
            Map.Entry<Integer, Integer> entry = entries.next();
            if(entry.getValue()==1)return entry.getKey();
        }
        return 0;
    }
}
```
- No.138 复制带随机指针的链表 **回溯**  
比较特殊的回溯
```
sclass Solution {
    HashMap<Node,Node> visited=new HashMap<Node,Node>();
    private Node copyRandomListCore(Node node){
        if(node==null)return null;
        if(visited.containsKey(node)){
            return visited.get(node);
        }
        Node root=new Node(node.val,null,null);
        visited.put(node,root);
        root.next=copyRandomListCore(node.next);
        root.random=copyRandomListCore(node.random);
        return root;
    }
    public Node copyRandomList(Node head) {
        return copyRandomListCore(head);
    }
}
```
