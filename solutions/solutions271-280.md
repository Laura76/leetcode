- No.271 **氪金**
- No.272 **氪金+困难**
- No.273 **困难**
- No.274 H指数
```
class Solution {
    public int hIndex(int[] citations) {
        int len=citations.length;
        int sum=0;
        for(int i=len;i>=0;i--){
            sum=0;
            for(int j:citations){
                if(j>=i){
                    sum++;
                }
            }
            if(sum>=i)return i;
        }
        return 0;
    }
}
```
- No.275 H指数II
```
class Solution {
    public int hIndex(int[] citations) {
        int len=citations.length;
        if(len==0)return 0;
        for(int i=len;i>0;i--){
            if(citations[len-i]>=i)return i;
        }
        return 0;
    }
}
```
- No.276 **氪金**
- No.277 **氪金**
- No.278 第一个错误的版本 **二分法**
```
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left=1,right=n;
        while(true){
            int temp=left+((right-left)>>1);            if(isBadVersion(temp)==false)left=temp+1;
            else right=temp-1;
            if(left>=right){              if(isBadVersion(right)==true)return right;
                else if(isBadVersion(left)==true)return left;
                return left+1;
            }
        }
    }
}
```



