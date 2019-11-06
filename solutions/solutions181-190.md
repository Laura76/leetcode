- No.181 超过经理收入的员工  **自连接**
```
/* Write your PL/SQL query statement below */
select e1.Name Employee
from Employee e1,Employee e2
where e1.ManagerId=e2.Id and e1.Salary>e2.Salary
```
- No.182 查找重复的电子邮箱  **自连接**
```
/* Write your PL/SQL query statement below */
select distinct p1.Email
from Person p1,Person p2
where p1.Id!=p2.Id and p1.Email=p2.Email
```
- No.183 从不订购的客户  **not in**
```
/* Write your PL/SQL query statement below */
select  c.Name Customers
from Customers c
where c.Id not in (select CustomerId from Orders
                  )
```
- No.184 部门工资最高的员工  **dense_rank**
```
/* Write your PL/SQL query statement below */
select Department,Employee,Salary
from(
select d.Name Department,e.Name Employee,e.Salary Salary ,
dense_rank()over(partition by e.DepartmentId order by e.Salary desc) rn
from Employee e,Department d
where e.DepartmentId=d.Id
)
where rn=1;
```
- No.185 部门工资前三高的所有员工  **dense_rank**
```
/* Write your PL/SQL query statement below */
select Department,Employee,Salary
from(
select d.Name Department,e.Name Employee,e.Salary Salary ,
dense_rank()over(partition by e.DepartmentId order by e.Salary desc) rn
from Employee e,Department d
where e.DepartmentId=d.Id
)
where rn<=3;
```
- No.186 翻转字符串里的单词 II  **两次翻转**
```
class Solution {
    public void reverseWords(char[] s) {
        //两次翻转
        int len=s.length;
        for(int i=0;i<len/2;i++){
            char temp=s[i];
            s[i]=s[len-1-i];
            s[len-1-i]=temp;
        }
        int space=0;
        for(int i=0;i<len;){
            while(space<len&&s[space]!=' ')space++;
            for(int j=i;j<i+(space-i)/2;j++){
                char temp=s[j];
                s[j]=s[space-1-j+i];
                s[space-1-j+i]=temp;
            }
            i=space+1;space++;
        }
    }
}
```
- No.187 重复的DNA序列  **理解题意**
```
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        int len=s.length();
        HashMap<String,Integer> map=new HashMap<String,Integer>();
        List<String> res=new ArrayList<String>();
        for(int i=0;i+10<=len;i++){
            String temp=s.substring(i,i+10);
            map.put(temp,map.getOrDefault(temp,0)+1);
            if(map.get(temp)==2)res.add(temp);
        }
        return res;
    }
}
```
- No.188 买卖股票的最佳时机  **困难**
- No.189 旋转数组  
```
class Solution {
    public void rotate(int[] nums, int k) {
        int len=nums.length;
        for(int i=1;i<=k;i++){
            int temp=nums[len-1];
            for(int j=len-1;j>0;j--){
                nums[j]=nums[j-1];
            }
            nums[0]=temp;
        }
    }
}
```
- No.190 颠倒二进制位  **位运算**
```
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int res=0;
        for(int i=0;i<=31;i++){
            int temp=n>>i;
            temp=temp&1;
            temp=(temp<<(31-i));
            res|=temp;
        }
        return res;
    }
}
```
