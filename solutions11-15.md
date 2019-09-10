- 第十一题 盛最多水的容器
```
class Solution {
    public int maxArea(int[] height) {
        int len=height.length;
        int front=0;
        int end=len-1;
        int width=end-front;
        int max=Math.min(height[front],height[end])*width;
        while(end>front){
            if(height[front]<height[end]){
                front++;
            }else{
                end--;
            }
            width=end-front;
            max=Math.max(max,Math.min(height[front],height[end])*width);
        }
        return max;
    }
}
```
