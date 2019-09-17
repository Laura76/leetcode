- 第四十一题 困难
- 第四十二题 困难
- 第四十三题 字符串相乘
```
class Solution {
    public String multiply(String num1, String num2) {
        if(num1.equals("0")||num2.equals("0"))return "0";
        int len1=num1.length();
        int len2=num2.length();
        int[] res=new int[len1+len2];
        for(int i=len1-1;i>=0;i--){
            for(int j=len2-1;j>=0;j--){
                int mul=(num1.charAt(i)-'0')*(num2.charAt(j)-'0');
                mul+=res[i+j+1];
                res[i+j]+=mul/10;
                res[i+j+1]=mul%10;
            }
        }
        StringBuilder strBuilder=new StringBuilder();
        boolean flag=false;
        for(int i:res){
            if(i==0&&flag==false){
                continue;
            }else if(i!=0&&flag==false){
                flag=true;
            }
            strBuilder.append(String.valueOf(i));
        }
        return strBuilder.toString();
    }
}
```
- 第四十四题 困难
- 第四十五题 困难
