- 第三十一题 下一个排列
```
class Solution {
    public void nextPermutation(int[] nums) {
        int len=nums.length;
        int i=len-1;
        for(;i>=1;i--){
            if(nums[i]>nums[i-1]){
                break;
            }
        }
        //已经是最大序列了即倒序序列
        if(i==0){
            reverse(nums);
            return;
        }
        for(int j=len-1;j>=i;j--){
            if(nums[j]>nums[i-1]){
                int temp=nums[i-1];
                nums[i-1]=nums[j];
                nums[j]=temp;
                break;
            }
        }        
        //倒置i后面的元素
        for(int j=i;j<(i+(len-i)/2);j++){
            int temp=nums[j];
            nums[j]=nums[i+len-1-j];
            nums[i+len-1-j]=temp;
        }
    }
    public void reverse(int[] nums){
        int len=nums.length;
        for(int i=0;i<len/2;i++){
            int temp=nums[i];
            nums[i]=nums[len-1-i];
            nums[len-1-i]=temp;
        }
    }
}
```
- 第三十二题 困难 不要啦
- 第三十三题 搜索旋转排序数组
```
class Solution {
    public int search(int[] nums, int target) {
        int start=0;
        int len=nums.length;
        int end=len-1;
        while(start<=end){
            int mid=start+((end-start)>>1);
            if(nums[mid]==target)return mid;
            if(nums[mid]>=nums[start]&&target<=nums[mid]&&target>=nums[start]){
                end=mid-1;
            }else if(nums[mid]>=nums[start]&&(target<nums[start]||target>nums[mid])){
                start=mid+1;
            }else if(nums[mid]<nums[start]&&target>nums[mid]&&target<=nums[end]){
                start=mid+1;
            }else{
                end=mid-1;
            }
        }
        return -1;
    }
}
```
- 第三十四题 在排序数组中查找元素的第一个和最后一个位置
```
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int len=nums.length;
        if(len==0)return new int[]{-1,-1};
        int[] res=new int[2];
        int start=0;
        int end=len-1;
        while(start<end){
            int mid=start+((end-start)>>1);
            if(nums[mid]==target){
                end=mid-1;
            }else if(nums[mid]>target){
                end=mid-1;
            }else if(nums[mid]<target){
                start=mid+1;
            }
        }
        if(nums[start]==target){
            res[0]=start;
        }else if(start+1<len&&nums[start+1]==target){
            res[0]=start+1;
        }else{
            res[0]=-1;
        }
        end=len-1;
        if(start==end){
            res[1]=res[0];
            return res;
        }
        while(start<end){
            int mid=start+((end-start)>>1);
            if(nums[mid]==target){
                start=mid+1;
            }else if(nums[mid]>target){
                end=mid-1;
            }else if(nums[mid]<target){
                start=mid+1;
            }
        }
        if(res[0]==-1){
            res[1]=-1;
        }else if(nums[start]==target){
            res[1]=start;
        }else{
            res[1]=start-1;
        }
        return res;
    }
}
```
- 第三十五题 搜索插入位置
```
class Solution {
    public int searchInsert(int[] nums, int target) {
        int len=nums.length;
        int start=0;int end=len-1;
        while(start<=end){
            int mid=start+((end-start)>>1);
            if(nums[mid]==target){
                return mid;
            }else if(nums[mid]>target){
                end=mid-1;
            }else if(nums[mid]<target){
                start=mid+1;
            }
        }
        if(start==0){
            return 0;
        }else if(start==len){
            return len;
        }
        if(nums[start]>target&&nums[end]>target){
            return Math.min(start,end);
        }else if(nums[start]>target){
            return start;
        }else if(nums[end]>target){
            return end;
        }
        return 0;
    }
}
```