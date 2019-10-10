- 第九十六题 不同的二叉搜索树
我真的爱死了动态规划，从小问题开始到大问题。真是很符合我这种头脑简单的人了。
```
class Solution {
    public int numTrees(int n) {
        int[] G=new int[n+1];
        G[0]=1;
        G[1]=1;
        for(int i=2;i<=n;i++){
            for(int j=0;j<=i-1;j++){
                G[i]+=G[j]*G[i-1-j];
            }
        }
        return G[n];
    }
}
```
- 第九十七题 交错字符串 困难 我好困啊啊
- 第九十八题 验证二叉搜索树 和搜索树就杠上了？
