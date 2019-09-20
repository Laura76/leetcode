- 第四十六题 全排列

**记住回溯的代码模版**

备注：每次递归都会传递的index是来计算已经使用了几个数字，当使用掉所有的数字就表示到达了叶节点。这个index只需要每次递归的时候加一就好了。

另外使用了布尔数组来判断数字是否使用过。

```
class Solution {
    private List<List<Integer>> res=new LinkedList<>();
    private boolean[] used;
    private int len;
    private int[] nums;

    private void permuteCore(int index,Stack<Integer> pre){
        if(index==len){
            res.add(new LinkedList<>(pre));
            return;
        }
        for(int i=0;i<len;i++){
            if(!used[i]){
                pre.push(nums[i]);
                used[i]=true;
                permuteCore(index+1,pre);
                pre.pop();
                used[i]=false;
            }
        }
    }
    public List<List<Integer>> permute(int[] nums) {
        int len=nums.length;
        this.len=len;
        this.nums=nums;
        used=new boolean[len];
        permuteCore(0,new Stack<>());
        return res;
    }
}
```
- 第四十七题 全排列Ⅱ
```
class Solution {
    private  List<List<Integer>> res=new LinkedList<>();
    private  boolean[] used;
    private int len;
    private int[] nums;
    private void permuteUniqueCore(int index,Stack<Integer> pre){
        if(index==len){
            res.add(new LinkedList<>(pre));
            return;
        }
        for(int i=0;i<len;i++){
            if(!used[i]){
                pre.push(nums[i]);
                used[i]=true;
                permuteUniqueCore(index+1,pre);
                pre.pop();
                used[i]=false;
                while(i+1<len&&nums[i]==nums[i+1]){
                    i++;
                }
            }
        }
    }
    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        this.nums=nums;
        int len=nums.length;
        this.len=len;
        used=new boolean[len];
        permuteUniqueCore(0,new Stack<>());
        return res;
    }
}
```
