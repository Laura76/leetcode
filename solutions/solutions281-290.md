- No.281 **氪金**
- No.282 **困难**
- No.283 移动零
```
class Solution {
    public void moveZeroes(int[] nums) {
        int len=nums.length;
        int click=len-1;
        for(int i=0;i<len;i++){
            if(click<i)break;
            if(nums[i]==0){
                for(int j=i;j<click;j++){
                    nums[j]=nums[j+1];
                }
                nums[click]=0;
                i=(len-1-click-1);
                click--;
            }
        }
    }
}
```
- No.284 顶端迭代器  
使用一个变量来记录peek，先拿下来保存着每次需要next的时候返回保存着的这个peek，接着更新这个peek变量。
```
// Java Iterator interface reference:
// https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html
class PeekingIterator implements Iterator<Integer> {
    private Iterator<Integer> myIterator;
    private Integer myPeek=null;
	public PeekingIterator(Iterator<Integer> iterator) {
	    // initialize any member here.
	    this.myIterator=iterator;
	}

    // Returns the next element in the iteration without advancing the iterator.
	public Integer peek() {
      if(myPeek==null&&myIterator.hasNext()){
          myPeek=myIterator.next();
      }
      return myPeek;
	}

	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	@Override
	public Integer next() {
        Integer res=peek();
        if(myIterator.hasNext()){
            myPeek=myIterator.next();
        }else{
            myPeek=null;
        }
        return res;
	}
	@Override
	public boolean hasNext() {
        return myPeek!=null||myIterator.hasNext();
	}
}
```
- No.285 **氪金**
- No.286 **氪金**
- No.287 寻找重复数  
尹总教的，每个数加上nums.length最后 被加了两次的下标就是答案。  
前提是数字在1-n之间。
```
class Solution {
    public int findDuplicate(int[] nums) {
        for(int i=0;i<nums.length;i++){
            int temp=nums[i]%nums.length;
            nums[temp]+=nums.length;
        }
        for(int i=0;i<nums.length;i++){
            if(nums[i]>(nums.length*2)){
                return i;
            }
        }
        return 0;
    }
}
```
- No.288 **氪金**
- No.289 生命游戏
```
class Solution {
    public void gameOfLife(int[][] board) {
        List<Integer> deadLive=new LinkedList<Integer>();
        List<Integer> liveDead=new LinkedList<Integer>();
        //12点开始顺时针
        int[] nextR={-1,-1,0,1,1,1,0,-1};
        int[] nextC={0,1,1,1,0,-1,-1,-1};
        int r=board.length;
        int c=board[0].length;
        for(int i=0;i<r;i++){
            for(int j=0;j<c;j++){
                if(board[i][j]==0){
                    int sum=0;
                    for(int k=0;k<8;k++){
                        int tempR=i+nextR[k],tempC=j+nextC[k];
                        if(tempR>=0&&tempR<r&&tempC>=0&&tempC<c){
                            if(board[tempR][tempC]==1)sum++;
                        }
                    }
                    //死细胞复活
                    if(sum==3){
                        deadLive.add(i);deadLive.add(j);
                    }
                }else{
                    int sum=0;
                    for(int k=0;k<8;k++){
                        int tempR=i+nextR[k],tempC=j+nextC[k];
                        if(tempR>=0&&tempR<r&&tempC>=0&&tempC<c){
                            if(board[tempR][tempC]==1)sum++;
                        }
                    }
                    //活细胞死亡
                    if(!(sum==2||sum==3)){
                        liveDead.add(i);liveDead.add(j);
                    }
                }
            }
        }
        for(int i=0;i<deadLive.size();i++){
            board[deadLive.get(i)][deadLive.get(i+1)]=1;
            i++;
        }
        for(int i=0;i<liveDead.size();i++){
            board[liveDead.get(i)][liveDead.get(i+1)]=0;
            i++;
        }
    }
}
```
- No.290 单词规律
```
class Solution {
    public boolean wordPattern(String pattern, String str) {
        int lenP=pattern.length();
        String[] words=str.split(" ");
        int lenS=words.length;
        if(lenP!=lenS)return false;
        char[] chars=pattern.toCharArray();
        //记录对应的关系
        HashMap<String,Character> map=new HashMap<String,Character>();
        int[] alphabet=new int[26];
        for(int i=0;i<lenS;i++){
            String temp=words[i];
            if(map.containsKey(temp)){
                //如果和之前已经记录的单词不符合的话，就返回false
                if(chars[i]!=map.get(temp) )return false;
            }else{
                alphabet[chars[i]-'a']++;
                if(alphabet[chars[i]-'a']==2)return false;
                map.put(temp,chars[i]);
            }
        }

        return true;
    }
}
```
