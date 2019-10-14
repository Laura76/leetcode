- No.131 分割回文串 **回溯**
```
class Solution {
    List<List<String>> res=new LinkedList<>();
    private int len=0;
    private String s;
    private void partitionCore(int curr,Stack<String> pre){
        if(curr==len){
            res.add(new ArrayList<>(pre));
            return;
        }
        for(int i=1;curr+i<=len;i++){
            String temp=s.substring(curr,curr+i);
            if(!isPali(temp))continue;
            pre.push(temp);
            partitionCore(curr+i,pre);
            pre.pop();
        }
    }
    public List<List<String>> partition(String s) {
        this.len=s.length();
        this.s=s;
        partitionCore(0,new Stack<String>());
        return res;
    }
    //判断回文
    private boolean isPali(String str){
        int start=0;
        int end=str.length()-1;
        while(start<end){
            if(str.charAt(start)!=str.charAt(end))return false;
            start++;end--;
        }
        return true;
    }
}
```
- No.132 分割回文串 II  **困难**
- No.133 克隆图 **回溯**
回溯的DFS递归，但是有点怪怪的，我自己找不到递归结束的终止条件，所以还是看一下简单的BFS的做法。
BFS的结束就很简单，访问过的节点就不加入队列，循环结束的条件是队列为空。每次遍历队列的时候，生成新的节点即可。
```
//DFS
class Solution {
    private HashMap<Integer,Node> map=new HashMap<Integer,Node>();
    private Node cloneGraphCore(Node node){
        if(map.containsKey(node.val)){
            return map.get(node.val);
        }
        Node root=new Node();
        root.val=node.val;
        root.neighbors=new ArrayList<>();
        map.put(root.val,root);
        for(Node n:node.neighbors){
            root.neighbors.add(cloneGraphCore(n));
        }
        return root;
    }
    public Node cloneGraph(Node node) {
        return cloneGraphCore(node);
    }
}
```
```
//BFS
class Solution {
    public Node cloneGraph(Node node) {
        if(node==null)return node;
        Queue<Node> q=new LinkedList<Node>();
        HashMap<Integer,Node> map=new HashMap<Integer,Node>();
        Set<Integer> visited=new HashSet<Integer>();
        q.add(node);
        visited.add(node.val);
        Node n=new Node();
        n.val=node.val;
        n.neighbors=new ArrayList<Node>();
        map.put(node.val,n);
        while(!q.isEmpty()){
            Node temp=q.remove();
            for(Node m:temp.neighbors){
                if(!map.containsKey(m.val)){
                    Node help=new Node();
                    help.val=m.val;
                    help.neighbors=new ArrayList<Node>();
                    map.put(m.val,help);
                }
                map.get(temp.val).neighbors.add(map.get(m.val));
                if(!visited.contains(m.val)){
                    visited.add(m.val);
                    q.add(m);
                }
            }
        }
        return map.get(node.val);
    }
}
```
- No.134 加油站
```
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int len=gas.length;
        //只有两个加油站的另外考虑
        if(len==1){
            return (gas[0]>=cost[0])?0:-1;
        }
        int[] weight=new int[len];
        for(int i=0;i<len;i++){
            weight[i]=gas[i]-cost[i];
        }
        for(int i=0;i<len;i++){
            if(weight[i]<0)continue;
            int temp=weight[i];
            for(int j=1;j<len;j++){
                if(temp+weight[(i+j)%len]<0)break;
                temp+=weight[(i+j)%len];
                if(j==len-1)return i;
            }
        }
        return -1;
    }
}
```
- No.135 分发糖果 **困难**
