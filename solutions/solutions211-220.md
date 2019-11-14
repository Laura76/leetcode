- No.211 添加与搜索单词 - 数据结构设计  **字典树/前缀树/TrieTree** **dfs**
```
public class TrieNode{
    private TrieNode[] links;
    private final int len=26;
    private boolean isEnd=false;
    public TrieNode(){
        this.links=new TrieNode[len];
    }
    public void setNode(int i){
        this.links[i]=new TrieNode();
    }
    public TrieNode getNode(int i){
        return this.links[i];
    }
    public void setEnd(){
        this.isEnd=true;
    }
    public boolean getEnd(){
        return this.isEnd;
    }
}
class WordDictionary {
    private TrieNode root;
    /** Initialize your data structure here. */
    public WordDictionary() {
        this.root=new TrieNode();
    }

    /** Adds a word into the data structure. */
    public void addWord(String word) {
        char[] chars=word.toCharArray();
        TrieNode node=root;
        for(char c:chars){
            if(node.getNode(c-'a')==null)node.setNode(c-'a');
            node=node.getNode(c-'a');
        }
        node.setEnd();
    }

    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    public boolean search(String word) {
        return dfs(root,word);
    }
    private boolean dfs(TrieNode node,String word){
        if(word.length()==0){
            return node.getEnd()==true;
        }
        char c=word.charAt(0);
        if(c=='.'){
            for(int i=0;i<26;i++){
                if(node.getNode(i)!=null&&dfs(node.getNode(i),word.substring(1))==true)return true;
            }
        }else{
            if(node.getNode(c-'a')!=null)return dfs(node.getNode(c-'a'),word.substring(1));
            else return false;
        }
        return false;
    }
}
/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```
- No.212. 单词搜索 II  **困难**
- No.213 打家劫舍Ⅱ  **dp**
```
class Solution {
    private int robCore(int[] nums,int left,int right){
        int[] dp=new int[right-left+1];
        int len=right-left+1;
        dp[0]=nums[left];if(len==1)return dp[0];
        dp[1]=Math.max(nums[left],nums[left+1]);if(len==2)return dp[1];
        for(int i=2;i<len;i++){
            dp[i]=Math.max(dp[i-1],dp[i-2]+nums[left+i]);
        }
        return dp[len-1];
    }
    public int rob(int[] nums) {
        int len=nums.length;
        if(len==0)return 0;
        if(len==1)return nums[0];
        if(len==2)return Math.max(nums[0],nums[1]);
        if(len==3)return Math.max(nums[2],Math.max(nums[0],nums[1]));
        return Math.max(robCore(nums,1,len-1),nums[0]+robCore(nums,2,len-2));
    }
}
```
- No.214 最短回文串  **困难**  
- No.215 数组中的第K个最大元素  
```
class Solution {
    public int findKthLargest(int[] nums, int k) {
        Arrays.sort(nums);
        return nums[nums.length-k];
    }
}
```
- No.216 组合总和 III  **dfs**
```
class Solution {
    private List<List<Integer>> res=new LinkedList<>();
    private boolean[] isVisit=new boolean[9];
    private void dfs(int level,int k,int sum,Stack<Integer> pre){
        if(level>k)return;
        if(level==k){
            if(sum==0){
                res.add(new LinkedList<>(pre));
            }
            return;
        }
        for(int i=1;i<=9&&isVisit[i-1]==false;i++){
            pre.push(i);isVisit[i-1]=true;
            dfs(level+1,k,sum-i,pre);
            pre.pop();isVisit[i-1]=false;
        }
    }
    public List<List<Integer>> combinationSum3(int k, int n) {
        dfs(0,k,n,new Stack<Integer>());
        return res;
    }
}
```
- No.217 存在重复元素  **哈希表**  
```
class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i:nums){
            map.put(i,map.getOrDefault(i,0)+1);
            if(map.get(i)>1)return true;
        }
        return false;
    }
}
```
- No.218 天际线问题  **困难**  
- No.219 存在重复元素 Ⅱ  
意思是只要存在两个索引差不超过K的数就行，所以找最小差就好了
```
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        if(nums.length==0)return false;
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        int diff=k+1;
        for(int i=0;i<nums.length;i++){
            if(map.containsKey(nums[i])){
                diff=Math.min(i-map.get(nums[i]),diff);
            }
            map.put(nums[i],i);
        }
        return diff<=k;
    }
}
```
- No.220 存在重复元素 III  **int超出界限**
```
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        int len=nums.length;
        for(int i=0;i<len-1;i++){
            int j=(i+k>=len)?len-1:i+k;
            for(;j>i;j--){
                if(Math.abs((long)nums[j]-(long)nums[i])<=t)return true;
            }
        }
        return false;
    }
}
```
