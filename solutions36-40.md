- 第三十六题 有效的数独
```
class Solution {
    public boolean isValidSudoku(char[][] board) {
        HashMap<Integer,Integer>[] rows=new HashMap[9];
        HashMap<Integer,Integer>[] columns=new HashMap[9];
        HashMap<Integer,Integer>[] boxes=new HashMap[9];
        for(int i=0;i<9;i++){
            rows[i]=new HashMap<Integer,Integer>();
            columns[i]=new HashMap<Integer,Integer>();
            boxes[i]=new HashMap<Integer,Integer>();
        }
        for(int i=0;i<9;i++){
            for(int j=0;j<9;j++){
                if(board[i][j]!='.'){
                    int num=board[i][j]-'0';
                    int boxIndex=(i/3)+(j/3)*3;
                    rows[i].put(num,rows[i].getOrDefault(num,0)+1);
                    columns[j].put(num,columns[j].getOrDefault(num,0)+1);
                    boxes[boxIndex].put(num,boxes[boxIndex].getOrDefault(num,0)+1);
                    if(rows[i].get(num)>1||columns[j].get(num)>1||boxes[boxIndex].get(num)>1){
                        return false;
                    }
                }
            }
        }
        return true;
    }
}
```
- 第三十七题 解数独 
困难 不要嘛
- 第三十八题 报数
```
class Solution {
    public String countAndSay(int n) {
        String str="1";
        int count=1;
        for(int i=1;i<n;i++){
            StringBuilder builder=new StringBuilder();
            char pre=str.charAt(0);
            for(int j=1;j<str.length();j++){
                char curr=str.charAt(j);
                if(curr==pre){
                    count++;
                }else{
                    builder.append(count).append(pre);
                    pre=curr;
                    count=1;
                }
            }
            builder.append(count).append(pre);
            str= builder.toString();
            count=1;
        }
        return str;
    }
}
```
- 第三十九题 组合总和

```
class Solution {
    private List<List<Integer>> res=new LinkedList<>();
    private int len;
    private int[] candidates;
    
    private void combinationSumCore(int currState,int start,Stack<Integer> pre){
        if(currState==0){
            res.add(new LinkedList<>(pre));
            return;
        }
        for(int i=start;i<len&&currState-candidates[i]>=0;i++){
            pre.push(candidates[i]);
            combinationSumCore(currState-candidates[i],i,pre);
            pre.pop();
        }
        
    }
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        Arrays.sort(candidates);
        this.len=candidates.length;
        this.candidates=candidates;
        combinationSumCore(target,0,new Stack<>());
        return res;
    }
}
```
- 第四十题 组合总数II
```
class Solution {
    private List<List<Integer>> res=new LinkedList<>();
    private int len;
    private int[] candidates;
    private void combinationSum2Core(int currState,int start,Stack<Integer> pre){
        if(currState==0){
            res.add(new LinkedList<>(pre));
            return;
        }
        for(int i=start;i<len&&currState-candidates[i]>=0;i++){
            pre.push(candidates[i]);
            combinationSum2Core(currState-candidates[i],i+1,pre);
            pre.pop();
            while(i+1<len&&candidates[i]==candidates[i+1]){
                i++;
            }
        }
    }
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        this.len=candidates.length;
        this.candidates=candidates;
        combinationSum2Core(target,0,new Stack<>() );
        return res;
    }
}
```
