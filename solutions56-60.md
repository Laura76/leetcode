- 第五十六题 合并区间
```
class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> res=new ArrayList<>();
        int len=intervals.length;
        if(len==1||len==0)return intervals;
        Arrays.sort(intervals,new myComparator());
        for(int i=0;i<len-1;i++){
            if(intervals[i][1]<intervals[i+1][0]){
                res.add(intervals[i]);
            }else{
                int left=intervals[i][0];
                int right=Math.max(intervals[i][1],intervals[i+1][1]);
                i++;
                while(i<len&&intervals[i][0]<=right){
                    right=Math.max(right,intervals[i][1]);
                    i++;
                }
                i--;
                res.add(new int[]{left,right});
            }
        }
        if(res.get(res.size()-1)[1]<intervals[len-1][0]){
            res.add(intervals[len-1]);
        }
        return res.toArray(new int[0][]);
    }
}
class myComparator implements Comparator<int[]>{
    @Override
    public int compare(int[] before,int[] end){
        if(before[0]==end[0]){
            if(before[1]==end[1]){
                return 0;
            }else{
                return before[1]>end[1]?1:-1;
            }
        }else{
            return before[0]>end[0]?1:-1;
        }
    }
}
```
- 第五十七题 插入区间 困难
- 第五十八题 最后一个单词的长度
```
class Solution {
    public int lengthOfLastWord(String s) {
        int len=s.length();
        int end=len-1;
        while(end>=0&&s.charAt(end)==' ')end--;
        if(end<0)return 0;
        int start=end;
        while(start>=0&&s.charAt(start)!=' ')start--;
        return end-start;
    }
}
```
- 第五十九题 螺旋矩阵Ⅱ
```
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] res=new int[n][n];
        int[] dr={0,1,0,-1};
        int[] dc={1,0,-1,0};
        int r=0,c=0,di=0;
        boolean[][] used=new boolean[n][n];
        for(int i=0;i<n*n;i++){
            res[r][c]=i+1;
            used[r][c]=true;
            int nr=r+dr[di];
            int nc=c+dc[di];
            if(nr>=0&&nr<n&&nc>=0&&nc<n&&!used[nr][nc]){
                r=nr;
                c=nc;
            }else{
                di=(di+1)%4;
                r+=dr[di];
                c+=dc[di];
            }
        }
        return res;
    }
}
```
- 第六十题 第K个排列
