- 第六十六题 加一
```
class Solution {
    public int[] plusOne(int[] digits) {
        int len=digits.length;
        int carry=1;
        for(int i=len-1;i>=0;i--){
            int temp=digits[i]+carry;
            if(temp<10){
                digits[i]=temp;
                return digits;
            }else{
                carry=1;
                digits[i]=temp%10;
            }
        }
        int[] res=new int[len+1];
        if(carry==1){
            res[0]=1;
            for(int i=1;i<res.length;i++){
                res[i]=digits[i-1];
            }
        }
        return res;
    }
}
```
- 第六十七题 二进制求和
```
class Solution {
    public String addBinary(String a, String b) {
        int aLen=a.length();
        int bLen=b.length();
        if(aLen<bLen)return addBinary(b,a);
        int carry=0;
        StringBuilder res=new StringBuilder();
        for(int i=1;i<=aLen;i++){
            int temp=(bLen-i>=0)?a.charAt(aLen-i)-'0'+carry+b.charAt(bLen-i)-'0': a.charAt(aLen-i)-'0'+carry;
            if(temp>=2){
                carry=1;
                res.append(String.valueOf(temp-2));
            }else{
                carry=0;
                res.append(String.valueOf(temp));
            }           
        }
        if(carry==1){
            res.append('1');
        }
        return res.reverse().toString();
    }
}
```
- 第六十八题 文本左右对齐
- 第六十九题 x的平方根
```
class Solution {
    public int mySqrt(int x) {
        //二分法
        if(x>=0&&x<1)return 0;
        if(x>=1&&x<4)return 1;
        if(x>46340*46340)return 46340;
        int left=2;
        int right=x/2+1;
        while(left<=right){
            int mid=Math.min(left+( (right-left)>>1 ) ,46340);
            int temp=mid*mid;
            if(temp==x)return mid;
            else if(temp>x){
                right=mid-1;
            }else{
                left=mid+1;
            }
        }
        if(left>right)left--;
        return left;
    }
}
```
- 第七十题 爬楼梯
//这样的不用写递归只写循环的动态规划真是让人太幸福了。
```
class Solution {
    public int climbStairs(int n) {
        int[] res=new int[n];
        if(n==0||n==1||n==2)return n;
        res[0]=1;
        res[1]=2;
        for(int i=2;i<n;i++){
            res[i]=res[i-1]+res[i-2];
        }
        return res[n-1];
    }
}
```
