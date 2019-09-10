- 第十一题 盛最多水的容器
```
class Solution {
    public int maxArea(int[] height) {
        int len=height.length;
        int front=0;
        int end=len-1;
        int width=end-front;
        int max=Math.min(height[front],height[end])*width;
        while(end>front){
            if(height[front]<height[end]){
                front++;
            }else{
                end--;
            }
            width=end-front;
            max=Math.max(max,Math.min(height[front],height[end])*width);
        }
        return max;
    }
}
```
- 第十二题 整转罗马数字
```
class Solution {
    public String intToRoman(int num) {
        int[] nums={1000,900,500,400,100,90,50,40,10,9,5,4,1};
        String[] latinNum={"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
        StringBuilder res=new StringBuilder();
        for(int i=0;i<13;i++){
            int sum=num/nums[i];
            for(int j=0;j<sum;j++){
                res.append(latinNum[i]);
            }
            num-=nums[i]*sum;
        }
        return res.toString();
    }
}
```
- 第十三题 罗马数字转整数
```
class Solution {
    public int romanToInt(String s) {
        Map<String,Integer> map=new HashMap<String,Integer>();
        map.put("I",1);
        map.put("IV",4);
        map.put("V",5);
        map.put("IX",9);
        map.put("X",10);
        map.put("XL",40);
        map.put("L",50);
        map.put("XC",90);
        map.put("C",100);
        map.put("CD",400);
        map.put("D",500);
        map.put("CM",900);
        map.put("M",1000);
        int i=0;
        int res=0;
        while(i<s.length()){
            if(i+1<s.length()){
                String temp=s.substring(i,i+2);
                if(map.containsKey(temp)){
                    res+=map.get(temp);
                    i+=2;
                }else{
                    res+=map.get(s.substring(i,i+1));
                    i++;
                }
            }else{
                res+=map.get(s.substring(i,i+1));
                i++;
            }
        }
        return res;
    }
}
```
- 第十四题 最长公共前缀
```
class Solution {
    public String longestCommonPrefix(String[] strs) {
        int len=strs.length;
        if(len==0)return "";
        if(strs[0].equals(""))return "";
        String res=strs[0];
        for(int i=1;i<len;i++){
            if(strs[i].equals(""))return "";
            res=compare(res,strs[i]);
        }
        return res;
    }
    //找出前缀
    public String compare(String str1,String str2){
        StringBuilder res=new StringBuilder();
        for(int i=0;i<str1.length()&&i<str2.length();i++){
            if(str1.charAt(i)==str2.charAt(i)){
                res.append(str1.charAt(i));
            }else{
                break;
            }
        }
        return res.toString();
    }
}
```
- 第十五题 三数之和