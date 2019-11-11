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
212. 单词搜索 II  **困难**
