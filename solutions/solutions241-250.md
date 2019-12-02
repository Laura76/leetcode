- No.241 为运算表达式设计优先级 **分治法**  
遍历每一个运算符：左边的结果数op右边的结果数，op指的是操作数。
```
class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        int len=input.length();
        List<Integer> res=new LinkedList<Integer>();
        if(!input.contains("+")&&!input.contains("-")&&!input.contains("*")){
            res.add(Integer.valueOf(input));
            return res;
        }
        for(int i=0;i<len;i++){
            char temp=input.charAt(i);
            if(temp=='+'||temp=='-'||temp=='*'){
                for(Integer left:diffWaysToCompute(input.substring(0,i))){
                    for(Integer right:diffWaysToCompute(input.substring(i+1))){
                        switch(temp){
                            case '+':
                                res.add(left+right);break;
                            case '-':
                                res.add(left-right);break;
                            case '*':
                                res.add(left*right);break;
                            default:break;
                        }
                    }
                }
            }
        }
        return res;
    }
}
```
- No.242 有效的字母异位词
```
class Solution {
    public boolean isAnagram(String s, String t) {
        HashMap<Character,Integer> mapS=new HashMap<Character,Integer>();
        for(Character c:s.toCharArray()){
            mapS.put(c,mapS.getOrDefault(c,0)+1);
        }
        for(Character c:t.toCharArray()){
            if(!mapS.containsKey(c))return false;
            mapS.put(c,mapS.get(c)-1);
        }
        for(Character c:s.toCharArray()){
            if(mapS.get(c)!=0)return false;
        }
        return true;
    }
}
```
- No.243-250 **氪金**
