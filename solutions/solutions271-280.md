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
- No.279 完全平方数 **记忆数组**  
注意：dp方法待做
```
class Solution {
    private boolean[] squareMemory;
    private int[] memory;
    private int core(int n){
        if(squareMemory[n]){
            memory[n]=1;
            return 1;
        }
        int count=1,start=1;
        while(start<=n){
            start=(count+1)*(count+1);
            count++;
        }
        start=(count-1)*(count-1);
        int res=Integer.MAX_VALUE;
        for(int i=start;(i>=1);i--){
            if(squareMemory[i]){
                int temp=0;
                if(memory[n-i]==0){
                    temp=core(n-i);
                }else{
                    temp=memory[n-i];
                }
                if(temp!=0)res=Math.min(res,temp+1);
            }
        }
        this.memory[n]=(res==Integer.MAX_VALUE?0:res);
        return memory[n];
    }
    public int numSquares(int n) {
        this.squareMemory=new boolean[n+1];
        for(int i=1;i<=n;i++){
            int temp=(int)Math.sqrt(i);
            squareMemory[i]=(temp*temp==i);
        }
        this.memory=new int[n+1];
        return core(n);
    }
}
```
- No.280 摆动排序 **氪金**



