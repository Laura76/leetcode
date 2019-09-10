- 6.
```
class Solution {

    public String convert(String s, int numRows) {
        if(numRows==1)return s;
        List<StringBuilder> rows=new ArrayList<>();
        for(int i=0;i<numRows;i++){
            rows.add(new StringBuilder());
        }
        int currRow=0;
        boolean direc=false;
        for(char c:s.toCharArray()){
            rows.get(currRow).append(c);
            if(currRow==0||currRow==numRows-1)direc=!direc;
            currRow+=direc==true?1:-1;
        }
        StringBuilder res=new StringBuilder();
        for(StringBuilder builder:rows){
            res.append(builder);
        }
        return res.toString();
    }
}
```
- 7.
```
class Solution {
    final double max=Math.pow(2,31)-1;
    final double min=-Math.pow(2,31);
    public int reverse(int x) {
        int res=0;
        if(x>=0){
            int[] bits=singleBit(x);
            int curr=bits[0];
            for(int i=1;i<bits.length;i++){
                int pop=bits[i];
                if(curr>max/10)return 0;
                else if(curr==max/10&&pop>7)return 0;
                curr=curr*10+pop;
            }
            res=curr;
        }else{
            int[] bits=singleBit(x);
            int curr=bits[0];
            for(int i=1;i<bits.length;i++){
                int pop=bits[i];
                if(curr<min/10)return 0;
                else if(curr==min/10&&pop<-8)return 0;
                curr=curr*10+pop;
            }
            res=curr;
        }
        return res;
    }

    //获得int的每一位
    public int[] singleBit(int x){
        List<Integer> bits=new ArrayList<Integer>();
        while(x/10!=0){
            bits.add(x%10);
            x=x/10;
        }
        bits.add(x);
        int[]  res=new int[bits.size()];
        for(int i=0;i<bits.size();i++){
            res[i]=bits.get(i);
        }
        return res;
    }
}
```
- 8.
```
class Solution {
    final int max=Integer.MAX_VALUE;
    final int min=Integer.MIN_VALUE;
    public int myAtoi(String str) {
        char[] chars=str.toCharArray();
        for(int i=0;i<chars.length;i++){
            if(chars[i]=='-'||chars[i]=='+'){
                boolean  posi=chars[i]=='+'?true:false;
                i++;
                if(i>=chars.length)return 0;
                if(chars[i]<'0'||chars[i]>'9')return 0;
                else{
                    List<Integer> num=new LinkedList<Integer>();
                    num.add(chars[i]-'0');
                    i++;
                    while(i<chars.length&&chars[i]>='0'&&chars[i]<='9'){
                        num.add(chars[i]-'0');
                        i++;
                    }
                    return posi==true?revert(num):revertNega(num);
                }
            }else if(chars[i]>='0'&&chars[i]<='9'){
                List<Integer> num=new LinkedList<Integer>();
                num.add(chars[i]-'0');
                i++;
                while(i<chars.length&&chars[i]>='0'&&chars[i]<='9'){
                    num.add(chars[i]-'0');
                    i++;
                }
                return revert(num);
            }else if(chars[i]!=' '){
                return 0;
            }
        }
        return 0;
    }
    public int  revert(List<Integer> num){
        int[] res=new int[num.size()];
        for(int i=0;i<num.size();i++){
            res[i]=num.get(i);
        }
        int curr=res[0];
        for(int i=1;i<res.length;i++){
            int pop=res[i];
            if(curr>max/10)return max;
            else if(curr==max/10&&pop>7)return max;
            curr=curr*10+pop;
        }
        return curr;
    }
    public int revertNega(List<Integer> num){
        int[] res=new int[num.size()];
        for(int i=0;i<num.size();i++){
            res[i]=num.get(i);
        }
        int curr=-res[0];
        for(int i=1;i<res.length;i++){
            int pop=-res[i];
            if(curr<min/10)return min;
            else if(curr==min/10&&pop<-8)return min;
            curr=curr*10+pop;
        }
        return curr;
    }
}
```
- 9.
```
class Solution {
    public boolean isPalindrome(int x) {
        if(x==0)return true;
        if(x<0)return false;
        int back=x%10;
        if(back==0)return false;
        x=x/10;
        while(x>back){
            back=back*10+x%10;
            x=x/10;
        }
        if(back==x||back/10==x)return true;
        else return false;
    }
}
```
- 10.s
