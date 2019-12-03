- No.281 **氪金**
- No.282 **困难**
- No.283 移动零
```
class Solution {
    public void moveZeroes(int[] nums) {
        int len=nums.length;
        int click=len-1;
        for(int i=0;i<len;i++){
            if(click<i)break;
            if(nums[i]==0){
                for(int j=i;j<click;j++){
                    nums[j]=nums[j+1];
                }
                nums[click]=0;
                i=(len-1-click-1);
                click--;
            }
        }
    }
}
```




