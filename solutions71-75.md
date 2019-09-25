- 第七十一题 简化路径
不懂规则是什么？？
- 第七十二题 编辑距离 困难模式
- 第七十三题 矩阵置零
我讨厌这种巨多细节的题目，尤其是被感冒侵袭的战斗力低下的我。
```
class Solution {
    public void setZeroes(int[][] matrix) {
        //判断第0列是否需要都置零
        boolean isZero=false;
        int R=matrix.length;
        if(R==0)return;
        int C=matrix[0].length;
        //遍历整个矩阵，如果某个元素是零的话，就 将其列首和行首的元素置为0
        //先处理一下两条边界
        //第0列 是否需要置零
        for(int i=0;i<R;i++){
            if(matrix[i][0]==0)isZero=true;
        }
        //第0行是否需要置零
        for(int i=0;i<C;i++){
            if(matrix[0][i]==0)matrix[0][0]=0;
        }

        for(int i=0;i<R;i++){
            for(int j=1;j<C;j++){
                if(matrix[i][j]==0){
                    matrix[i][0]=0;
                    matrix[0][j]=0;
                }    
            }
        }
        //开始我的修改矩阵的大路

        //再遍历一下所有的行首和列首
         for(int i=1;i<C;i++){
            if(matrix[0][i]==0){
                for(int j=0;j<R;j++){
                    matrix[j][i]=0;
                }
            }
        }
        for(int i=0;i<R;i++){
            if(matrix[i][0]==0){
                for(int j=0;j<C;j++){
                    matrix[i][j]=0;
                }
            }
        }

        //说明第0行 需要置零
        if(matrix[0][0]==0){
            for(int i=0;i<C;i++){
                matrix[0][i]=0;
            }
        }
        if(isZero==true){
            for(int i=0;i<R;i++){
                matrix[i][0]=0;
            }
        }
    }
}
```
- 第七十四题 搜索二维矩阵
这道题很是小甜心呀。真好，这才适合我这种壮汉。好吧，我发现自己已经有浪的前兆了。不，我不可以
```
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int R=matrix.length;
        if(R==0)return false;
        int C=matrix[0].length;
        int r=0;
        int c=C-1;
        while(r>=0&&r<R&&c>=0&&c<C){
            if(matrix[r][c]>target){
                c--;
            }else if(matrix[r][c]==target){
                return true;
            }else{
                r++;
            }
        }
        return false;

    }
}
```
- 第七十五题 颜色分类
```
class Solution {
    public void sortColors(int[] nums) {
        int len=nums.length;
        if(len==0)return;
        int p0=0;
        int curr=0;
        int p2=len-1;
        while(curr<=p2){
            if(nums[curr]==2){
                nums[curr]=nums[p2];
                nums[p2]=2;
                p2--;
            }else if(nums[curr]==1){
                curr++;
            }else if(nums[curr]==0){
                nums[curr]=nums[p0];
                nums[p0]=0;
                curr++;
                p0++;
            }
        }
    }
}
```
