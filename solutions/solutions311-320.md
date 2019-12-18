- No.311 **氪金**
- No.312 **困难**
- No.313 超级丑数  **暂时不想做数学题**
- No.314 **氪金**
- No.315 **困难**
- No.316 **困难**
- No.317 **困难**
- No.318 最大单词长度乘积  
感觉套路只针对适合它的典型案例，找不到什么套路的时候就按照正常想法来做
```
class Solution {
    //判断两个字符串是否含有公共的字母
    private boolean hasCommon(String a,String b){
        for(int i=0;i<a.length();i++){
            char temp=a.charAt(i);
            for(int j=0;j<b.length();j++){
                while(j<b.length()&&b.charAt(j)<temp)j++;
                if(j>=b.length())break;
                if(b.charAt(j)==temp)return true;
                else if(b.charAt(j)>temp)break;
            }
        }
        return false;
    }
    //将字符串变为字典正序
    private String revert(String str){
        char[] temp=str.toCharArray();
        Arrays.sort(temp);
        StringBuilder builder=new StringBuilder();
        for(char c:temp)builder.append(c);
        return builder.toString();
    }
    public int maxProduct(String[] words) {
        //先排序再遍历
        Arrays.sort(words,new Comparator <String>(){
		    public int compare(String a, String b){
			    int lenA=a.length();
                int lenB=b.length();
                return lenA-lenB;
			}
		});
        //将所有字符串变为正序
        for(int i=0;i<words.length;i++){
            words[i]=revert(words[i]);
        }
        int res=0;
        //每个单词遍历比较，从后往前比较，后面的比较大
        for(int i=words.length-1;i>=1;i--){
            for(int j=i-1;j>=0;j--){
                if(!hasCommon(words[i],words[j])){
                    res=Math.max(res,words[i].length()*words[j].length());
                }
            }
        }
        return res;

    }
}
```
- No.319 灯泡开关  
### 解题思路
可以看作是从1到n,每次都是按照规则：每i个切换状态。初始状态是all 灭。  
所求的n次之后亮的灯泡，则该灯泡要经过奇数次切换即有奇数个公约数。  
A有奇数个公约数意味着必有两个相同的公约数相乘得到A，即所谓的完全平方数  
题目就变成了求1-n的完全平方数的个数，就是floor(sqrt(n));  
### 代码
```java
class Solution {
    public int bulbSwitch(int n) {
        return (int)Math.sqrt(n);
    }
}
```
- No.320 **氪金**
