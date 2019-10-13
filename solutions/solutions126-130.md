- No.126 单词接龙II **困难**
- No.127 单词接龙
```
import javafx.util.Pair;
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        HashMap<String,ArrayList<String>> map=new HashMap<String,ArrayList<String>>();
        int level=0;
        for(String str:wordList){
            for(int i=0;i<str.length();i++){
                String temp=str.substring(0,i)+"*"+str.substring(i+1);
                ArrayList<String> strs=map.getOrDefault(temp,new ArrayList<String>());
                strs.add(str);
                map.put(temp,strs);
            }
        }
        Queue<Pair<String,Integer>> q=new LinkedList<>();
        q.add(new Pair(beginWord,1));
        HashMap<String,Boolean> visited=new HashMap<String,Boolean>();
        visited.put(beginWord,true);
        while(!q.isEmpty()){
            Pair<String,Integer> temp=q.remove();
            String key=temp.getKey();
            level=temp.getValue();
            for(int i=0;i<key.length();i++){
                String temp2=key.substring(0,i)+"*"+key.substring(i+1);
                for(String str:map.getOrDefault(temp2,new ArrayList<String>())){
                    if(str.equals(endWord)){
                        return level+1;
                    }
                    if(!visited.getOrDefault(str,false) ){
                        q.add(new Pair(str,level+1));
                        visited.put(str,true);
                    }
                }
            }
        }
        return 0;
    }
}
```