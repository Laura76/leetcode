- No.171. Excel Sheet Column Number
```
class Solution {
    public int titleToNumber(String s) {
        HashMap<Character,Integer> map=new HashMap<Character,Integer>();
        for(int i=0;i<26;i++){
            map.put((char)(65+i),i+1);
        }
        int len=s.length();
        int res=0;
        for(int i=0;i<len;i++){
            res+=map.get(s.charAt(i))*Math.pow(26,len-1-i);
        }
        return res;
    }
}
```
- No.172 阶乘后的零 **数学**
- No.173 二叉搜索树迭代器  **栈**
```
class BSTIterator {
    Stack<Integer> stack=new Stack<Integer>();
    private void BSTIteratorCore(TreeNode node){
        if(node.right!=null){
            BSTIteratorCore(node.right);
        }
        stack.push(node.val);
        if(node.left!=null){
            BSTIteratorCore(node.left);
        }
    }
    public BSTIterator(TreeNode root) {
        if(root!=null)BSTIteratorCore(root);
    }    
    /** @return the next smallest number */
    public int next() {
        return stack.pop();
    }    
    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return (stack!=null)&&(!stack.isEmpty());
    }
}
/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```
- No.174 地下城游戏 **困难**
- No.175 组合两个表  **Oraclesql**
```
/* Write your PL/SQL query statement below */
select p.FirstName,p.LastName,addr.City,addr.State
from Person p left join Address addr
on p.PersonId=addr.PersonId
```
- No.176 第二高的薪水 **Oraclesql** **row_number**
```
/* Write your PL/SQL query statement below */
select min(Salary) SecondHighestSalary
from (select Salary,row_number() over(order by Salary desc) rn
      from (select distinct Salary from Employee)
      )
where rn!=1 and rn<=2
```
- No.177 第N高的薪水  **row_number**
```
CREATE FUNCTION getNthHighestSalary(N IN NUMBER) RETURN NUMBER IS
result NUMBER;
BEGIN
    /* Write your PL/SQL query statement below */
    select Salary into result
    from (select Salary,row_number()over(order by Salary desc) rn
         from (select distinct Salary from Employee) )
    where rn=N ;
    RETURN result;
END;
```
- No.178 分数排名  **dense_rank**
```
/* Write your PL/SQL query statement below */
select Score,dense_rank()over(order by Score desc) Rank
from Scores
```
- No.179 最大数  **comparator接口**
```
class Solution {
    private class myComparator implements Comparator<String>{
        @Override
        public int compare(String a,String b){
            String s1=a+b;
            String s2=b+a;
            return s2.compareTo(s1);
        }
    }
    public String largestNumber(int[] nums){
        int len=nums.length;
        String[] strs=new String[len];
        for(int i=0;i<len;i++)strs[i]=String.valueOf(nums[i]);
        Arrays.sort(strs,new myComparator());
        StringBuilder builder=new StringBuilder();
        for(String str:strs)builder.append(str);
        return builder.charAt(0)=='0'?"0":builder.toString();
    }
}
```
- No.180 连续出现的数字  **注意连续**
```
select distinct a.Num ConsecutiveNums
from Logs a,Logs b,Logs c
where a.Id=b.Id-1 and b.Id=c.Id-1 and
a.Num=b.Num and b.Num=c.Num
```
