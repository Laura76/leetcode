- No.116 填充每个节点的下一个右侧节点指针  
```
class Solution {
    public Node connect(Node root) {
        Node pre=root;
        while(pre!=null){
            Node curr=pre;
            while(curr!=null){
                if(curr.left!=null)curr.left.next=curr.right;
                if(curr.right!=null&&curr.next!=null)curr.right.next=curr.next.left;
                curr=curr.next;
            }
            pre=pre.left;
        }
        return root;
    }
}
```
- No.117 填充每个节点的下一个右侧节点指针 II
```
class Solution {
    public Node connect(Node root) {
        Node pre=root;
        while(pre!=null){
            Node curr=pre;
            while(curr!=null){
                if(curr.left!=null&&curr.right!=null)curr.left.next=curr.right;
                else if(curr.left!=null&&curr.next!=null){
                    Node temp=curr.next;
                    while(temp!=null){
                        if(temp.left!=null){
                            curr.left.next=temp.left;
                            break;
                        }
                        if(temp.right!=null){
                            curr.left.next=temp.right;
                            break;
                        }
                        temp=temp.next;
                    }
                }
                if(curr.right!=null&&curr.next!=null){
                    Node temp=curr.next;
                    while(temp!=null){
                        if(temp.left!=null){
                            curr.right.next=temp.left;
                            break;
                        }
                        if(temp.right!=null){
                            curr.right.next=temp.right;
                            break;
                        }
                        temp=temp.next;
                    }
                }
                curr=curr.next;
            }
            while(pre!=null){
                if(pre.left!=null){
                    pre=pre.left;
                    break;
                }
                if(pre.right!=null){
                    pre=pre.right;
                    break;
                }
                pre=pre.next;
            }
        }
        return  root;
    }
}
```

- No.118 杨辉三角  
```
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res=new LinkedList<>();
        if(numRows==0)return res;
        res.add(new ArrayList<Integer>() {{add(1);}} );
        if(numRows==1)return res;
        res.add(new ArrayList<Integer>() {{add(1);add(1);}} );
        for(int i=2;i<numRows;i++){
            res.add(new ArrayList<Integer>() {{add(1);}} );
            for(int j=0;j<res.get(i-1).size()-1;j++){
                res.get(i).add(res.get(i-1).get(j)+res.get(i-1).get(j+1));
            }
            res.get(i).add(1);
        }
        return res;
    }
}
```
- No.119 杨辉三角Ⅱ
```
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> pre=new ArrayList<>();
        List<Integer> curr;
        pre.add(1);
        if(rowIndex==0)return pre;
        for(int i=1;i<=rowIndex;i++){
            curr=new ArrayList<>();
            curr.add(1);
            for(int j=0;j<pre.size()-1;j++){
                curr.add(pre.get(j)+pre.get(j+1));
            }
            curr.add(1);
            pre=curr;
        }
        return pre;
    }
}
```
- No.120 三角形最小路径和 **自底向上的动态规划**
和求简单的路径和的动态规划的思考方式有类似之处。
```
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        int row=triangle.size();
        int[] nums=new int[row+1];
        for(int i=row-1;i>=0;i--){
            for(int j=0;j<i+1;j++){
                nums[j]=Math.min(nums[j],nums[j+1])+triangle.get(i).get(j);
            }
        }
        return nums[0];
    }
}
```
