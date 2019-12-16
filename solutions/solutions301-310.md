- No.301 **困难**
- No.302 **困难**
- No.303 区域和检索 - 数组不可变 **好奇怪的题目**
```
class NumArray {
    private int[] nums;
    public NumArray(int[] nums) {
        this.nums=nums;
    }

    public int sumRange(int i, int j) {
        int res=0;
        for(int k=i;k<=j;k++){
            res+=this.nums[k];
        }
        return res;
    }
}
/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(i,j);
 */
```
-  No.304 二维区域和检索 - 矩阵不可变 **保存中间的结果，参照上一题的**
```
class NumMatrix {
    private int[][] results;
    public NumMatrix(int[][] matrix) {
        int r=matrix.length;
        if(r==0)return;
        int c=matrix[0].length;
        this.results=new int[r][c];
        for(int i=0;i<r;i++){
            for(int j=0;j<c;j++){
                if(j==0)this.results[i][0]=matrix[i][j];
                else this.results[i][j]=matrix[i][j]+this.results[i][j-1];
            }
        }
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        int res=0;
        for(int i=row1;i<=row2;i++){
            if(col1-1<0)res+=this.results[i][col2];
            else res+=this.results[i][col2]-this.results[i][col1-1];
        }
        return res;
    }
}
/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix obj = new NumMatrix(matrix);
 * int param_1 = obj.sumRegion(row1,col1,row2,col2);
 */
```
- No.305 岛屿数量 **氪金** **困难**
- No.306 累加数
```
class Solution {
    //给定第一个和第二个数字，判断是否是累加序列
    private boolean core(int s1,int end1,int s2,int end2,String num){
        if(end2>=num.length())return true;
        String first=num.substring(s1,end1);
        String sec=num.substring(s2,end2);
        long sum=Long.valueOf(first)+Long.valueOf(sec);
        if(num.substring(end2).startsWith(String.valueOf(sum))){
            return core(s2,end2,end2,end2+String.valueOf(sum).length(),num);
        }else{
            return false;
        }
    }
    public boolean isAdditiveNumber(String num) {
        int len=num.length();
        if(len<3)return false;
        //处理一下第一个数字是1的情况
        if(num.charAt(0)=='0'){
            //如果第二个也是0
            if(num.charAt(1)=='0'){
                return core(0,1,1,2,num);
            }else{
                for(int i=2;i<=len-1;i++){
                    return core(0,1,1,i,num);
                }
            }      
        }
        //先遍历第一个
        for(int i=1;i<=len-2;i++){
            String first=num.substring(0,i);
            //考虑第二个数字是0的情况
            if(num.charAt(i)=='0') {
                if( core(0,i,i,i+1,num)==true )return true;
            }
            //再寻找第二个数
            else{
                for(int j=i+1;j<=len-1;j++){
                    String sec=num.substring(i,j);
                    if(core(0,i,i,j,num)==true){
                        return true;
                    }
                }
            }
        }
        return false;
    }
}
```
- No.307 区域和检索 - 数组可修改
```
class NumArray {
    private int[] result;
    private int[] myNums;
    public NumArray(int[] nums) {
        this.myNums=nums;
        int len=nums.length;
        this.result=new int[len];
        for(int i=0;i<len;i++){
            if(i==0)this.result[i]=nums[i];
            else this.result[i]=this.result[i-1]+nums[i];
        }
    }

    public void update(int i, int val) {
        for(int j=i;j<this.result.length;j++){
            if(j==i){
                if(i==0)this.result[i]=val;
                else this.result[i]=this.result[j-1]+val;
            }
            else this.result[j]=this.result[j-1]+myNums[j];
        }
        myNums[i]=val;
    }

    public int sumRange(int i, int j) {
        if(i==0)return this.result[j];
        else return this.result[j]-this.result[i-1];
    }
}
/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```
- No.308 **困难**
