4、leetcode459. 重复的子字符串
==
解法一：
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
解法二： 
--
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/14 14:58
 * @descriptor  459. 重复的子字符串
 */
public class RepeatedSubstringPattern_459 {
    //利用StringAPI，如果全是重复的子字符串，那么使用split函数拆分后的数组长度将会是0
    //找字符串长度的因子，挨个去拆分出子串，去测试满足split函数拆分的数组长度是否为0
    //split函数使用的规则是正则匹配，效率略低
    public static boolean repeatedSubstringPattern(String s) {
        // 判断鲁棒性
        if (s == null || s.length() < 2)
            return false;
        // 长度大于1，可以拆分出子串，判断字符串中是否所有字符都相同，如"aaaaaa","zzz"，一定满足按子串长度为1的拆分，所以直接返回true
        if(s.split(String.valueOf(s.charAt(0))).length == 0)
            return true;
        for (int i = s.length()/2; i > 1; i--) {
            if(s.length() % i == 0){
                String substring = s.substring(0, i);
                String[] split = s.split(substring);
                if(split.length == 0)
                    return true;
            }
        }
        return false;
    }
    public static void main(String[] args) {
        String s = "abcabcabc";
        boolean b = repeatedSubstringPattern3(s);
        System.out.println(b);
    }
}
</pre>
解法三：  
--   
代码： 
--
<pre>
/**
 * @author lihe
 * @date 2019/10/14 14:58
 * @descriptor  459. 重复的子字符串
 */
public class RepeatedSubstringPattern_459 {
    //1.将原字符串给出拷贝一遍组成新字符串；
    //2.掐头去尾留中间；
    //3.如果还包含原字符串，则满足题意。
    public static boolean repeatedSubstringPattern3(String s) {
        String strings = s + s;
        String substring = strings.substring(1, strings.length() - 1);
        if(substring.contains(s))
            return true;
        else
            return false;
    }

    public static void main(String[] args) {
        String s = "abcabcabc";
        boolean b = repeatedSubstringPattern3(s);
        System.out.println(b);
    }
}
</pre>



