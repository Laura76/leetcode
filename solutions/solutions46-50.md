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
- 第四十八题 旋转图像
```
class Solution {
    public void rotate(int[][] matrix) {
        int n=matrix.length;
        for(int i=0;i<=n/2-1;i++){
            int len=n-1-i*2;
            for(int j=0;j<len;j++){
                int temp=matrix[i+j][n-1-i];
                matrix[i+j][n-1-i]=matrix[i][i+j];
                matrix[i][i+j]=matrix[n-1-i-j][i];
                matrix[n-1-i-j][i]=matrix[n-1-i][n-1-i-j];
                matrix[n-1-i][n-1-i-j]=temp;
            }
        }
    }
}
```
- 第四十九题 字母异序词分组
```
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        int len=strs.length;
        if(len==0)return new ArrayList<>();
        Map<String,List<String>> map=new HashMap<String,List<String>>();
        for(String s:strs){
            char[] ca=s.toCharArray();
            Arrays.sort(ca);
            String key=String.valueOf(ca);
            if(!map.containsKey(key)){
                map.put(key,new ArrayList<String>());
            }
            map.get(key).add(s);
        }
        return new ArrayList<>(map.values());
    }
}
```
- 第五十题 Pow(x,n)
```
class Solution {
    public double myPowCore(double x,long N ){
        if(N==0){
            return 1.0;
        }
        double half=myPowCore(x,N/2);
        if(N%2==0){
            return half*half;
        }else{
            return half*half*x;
        }
    }
    public double myPow(double x, int n) {
        long N=n;
        if(n<0){
            x=1/x;
            N=-N;
        }
        return myPowCore(x,N);
    }
}
```