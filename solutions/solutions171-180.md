- No.171. Excel Sheet Column Number
```
class Solution {
    public int titleToNumber(String s) {
        HashMap<Character,Integer> map=new HashMap<Character,Integer>();
        for(int i=0;i<26;i++){
            map.put((char)(65+i),i+1);
        }
        int len=s.length();
        int res=0;
        for(int i=0;i<len;i++){
            res+=map.get(s.charAt(i))*Math.pow(26,len-1-i);
        }
        return res;
    }
}
```