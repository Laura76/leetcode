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
动态规划 呃呃呃呃呃 等会再说，不适合生病的我   
- 第四十题 组合总和Ⅱ
原因同上 
