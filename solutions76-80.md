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
