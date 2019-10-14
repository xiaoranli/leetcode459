4、leetcode459. 重复的子字符串
==
解法一：水平扫描  
--
思路：
--
    解题思路：字符串是由重复子串构成，说明重复子串的length必定小于等于源字符串的一半，还有就是s.length() % length == 0。所以，把子串的长度初始化为s.length()/2，然后循环判断。时间复杂度为：O(n)。    
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/14 14:58
 * @descriptor  459. 重复的子字符串
 */
public class RepeatedSubstringPattern_459 {

    //从一半字符串开始判断，如果是长度的倍数说明是重复多次得到
    //然后算出重复的次数，累加出长度相等的字符串，然后比较
    public static boolean repeatedSubstringPattern(String s) {
        // 判断鲁棒性
        if(s == null || s.length() < 2)
            return false;
        for (int i = s.length()/2; i > 0; i--) {
            // 判断是否满足重复子串
            if(s.length() % i == 0){
                StringBuilder builder = new StringBuilder();
                // 得到重复子串的个数
                int count = s.length() / i;
                for (int j = 0; j < count; j++) {
                    builder.append(s.substring(0,i));
                }
                if(builder.toString().equals(s))
                    return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        String s = "abcabcabc";
        boolean b = repeatedSubstringPattern(s);
        System.out.println(b);
    }
}
</pre>
