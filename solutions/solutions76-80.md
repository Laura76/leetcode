- 第七十六题 最小覆盖字串 困难模式
- 第七十七题 组合
现在完全不畏惧简单的回溯问题，只是执行时间并不是很优
```
class Solution {
    private int n;
    private int k;
    private int[] nums;
    private List<List<Integer>> res=new ArrayList<>();
    private void combineCore(Stack<Integer> pre,int depth,int posi){
        if(depth==k){
            res.add(new ArrayList<>(pre));
            return;
        }
        for(int i=posi;i<n;i++){
            pre.push(nums[i]);
            combineCore(pre,depth+1,i+1);
            pre.pop();
        }
    }
    public List<List<Integer>> combine(int n, int k) {
        this.n=n;
        this.k=k;
        this.nums=new int[n];
        for(int i=0;i<n;i++){
            nums[i]=i+1;
        }
        combineCore(new Stack<Integer>(),0,0);
        return res;
    }
}
```
- 第七十八题 子集
```
class Solution {
    private int len;
    private int[] nums;
    private List<List<Integer>> res=new ArrayList<>();
    private void subsetsCore(Stack<Integer> pre,int posi){
        if(posi>=len){
            return;
        }
        for(int i=posi;i<len;i++){
            pre.push(nums[i]);
            res.add(new ArrayList<>(pre));
            subsetsCore(pre,i+1);
            pre.pop();
        }
    }
    public List<List<Integer>> subsets(int[] nums) {
        this.len=nums.length;
        this.nums=nums;
        subsetsCore(new Stack<Integer>(),0);
        res.add(new ArrayList<>());
        return res;
    }
}
```
- 第七十九题 单词搜索
```
class Solution {
    private int R;
    private int C;
    private char[] target;
    private int[] dr={0,1,0,-1};
    private int[] dc={1,0,-1,0};
    private boolean[][] used;
    private boolean existCore(int depth,int r,int c,char[][] board){
        if(depth==target.length-1){
            return true;
        }
        for(int i=0;i<4;i++){
            int nr=r+dr[i];
            int nc=c+dc[i];
            if(nr>=0&&nr<R&&nc>=0&&nc<C&&!used[nr][nc]){
                if(board[nr][nc]==target[depth+1]){
                    used[nr][nc]=true;
                    if(existCore(depth+1,nr,nc,board)){
                        return true;   
                    }else{
                        used[nr][nc]=false;
                    }
                }
            }
        }
        return false;
    }
    public boolean exist(char[][] board, String word) {
        this.target=word.toCharArray();
        this.R=board.length;
        if(this.R==0)return false;
        this.C=board[0].length;
        this.used=new boolean[R][C];
        for(int i=0;i<R;i++){
            for(int j=0;j<C;j++){
                if(board[i][j]==this.target[0]){
                    used[i][j]=true;
                    if(existCore(0,i,j,board))return true;
                    used[i][j]=false;
                }
            }
        }
        return false;
    }
}
```
- 第八十题 删除排序数组中的重复项Ⅱ
```
class Solution {
    public int removeDuplicates(int[] nums) {
        int len=nums.length;
        int pr=0;
        int count=1;
        for(int i=1;i<len;i++){
            if(nums[i]==nums[pr]){
                if(count<2){
                    nums[++pr]=nums[i];
                    count++;
                }
            }else{
                nums[++pr]=nums[i];
                count=1;
            }
        }
        return pr+1;
    }
}
```
