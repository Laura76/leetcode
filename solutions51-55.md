
- 第五十一题 N皇后 想起大二的噩梦
- 第五十二题 N皇后Ⅱ
- 第五十三题 最大子序和
```
class Solution {
    public int maxSubArray(int[] nums) {
        int res=nums[0];
        int sum=0;
        for(int i=0;i<nums.length;i++){
            if(sum>0){
                sum+=nums[i];
            }else{
                sum=nums[i];
            }
            res=Math.max(res,sum);
        }
        return res;
    }
}
```
- 第五十四题 螺旋矩阵
```
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> res=new ArrayList<>();
        int R=matrix.length;
        if(R==0)return res;
        int C=matrix[0].length;
        int[] dr={0,1,0,-1};
        int[] dc={1,0,-1,0};
        int r=0,c=0,di=0;
        boolean[][] used=new boolean[R][C];
        for(int i=0;i<R*C;i++){
            res.add(matrix[r][c]);
            used[r][c]=true;
            int nr=r+dr[di];
            int nc=c+dc[di];
            if(nr>=0&&nr<R&&nc>=0&&nc<C&&!used[nr][nc]){
                r=nr;
                c=nc;
            }else{
                di=(di+1)%4;
                r=r+dr[di];
                c=c+dc[di];
            }
        }
        return res;
    }
}
```
- 第五十五题 跳跃游戏
```
enum State{GOOD,BAD,UNUSED}
class Solution {
    private State[] went;
    private int[] nums;
    private int len;
    private boolean canJumpCore(int posi){
        if(went[posi]!=State.UNUSED){
            return went[posi]==State.GOOD?true:false;
        }
        int edge=Math.min(posi+nums[posi],len-1);
        for(int i=posi+1;i<=edge;i++){
            if(canJumpCore(i)){
                went[posi]=State.GOOD;
                return true;
            }
        }
        went[posi]=State.BAD;
        return false;
    }
    public boolean canJump(int[] nums) {
        this.len=nums.length;
        this.nums=nums;
        this.went=new State[len];
        for(int i=0;i<len;i++){
            went[i]=State.UNUSED;
        }
        went[len-1]=State.GOOD;
        return canJumpCore(0);
    }
}
```
