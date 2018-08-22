# String

## 1 数字运算

**(1) 用字符串模拟两个大数相加**

- 反转两个字符串，便于从低位到高位相加和最高位的进位导致和的位数增加
- 对齐两个字符串，即短字符串的高位用‘0’补齐，便于后面的相加
- 把两个正整数相加，一位一位的加并加上进位

```java
public class AddSum {
    public static void main(String[] args)
    {
        String s1 = "12345";
        String s2 = "53456";
        AddSum as = new AddSum();
        System.out.println(as.addSum(s1, s2));
    }

    public String addSum(String s1, String s2)
    {
        StringBuilder result = new StringBuilder();

        s1 = new StringBuilder(s1).reverse().toString();
        s2 = new StringBuilder(s2).reverse().toString();

        int len1 = s1.length();
        int len2 = s2.length();
        int maxLen = len1 > len2 ? len1 + 1: len2+1;
        if(len1 > len2) {
            for(int i = len2; i < maxLen; i++)
                s2 += "0";
            s1 += "0";
        }
        else {
            for (int i = len1; i < maxLen; i++)
                s1 += "0";
            s2 += "0";
        }

        boolean isCarry = false;
        for(int i = 0; i < maxLen; i++)
        {
            int sum = Integer.parseInt(s1.charAt(i) + "") + Integer.parseInt(s2.charAt(i) + "");
            if(isCarry)
                sum += 1;
            if(sum >= 10)
                isCarry = true;
            else
                isCarry = false;
            result.append(sum%10);
        }

        return result.reverse().toString().replaceAll("^0", "");
    }
}
```

## 2 排序、交换

**(1) 把一个0-1串(只包含0和1的串)进行排序，你可以交换任意两个位置，问最少交换的次数**

**(2) 一个字符串只包含\*和数字，请把它的\*都放到开头**

## 3 字符计数

**(1) 给定两个串a和b，问b是不是a的字串的变位词。例如输入a=hello，b=lel，lle，ello都是true，但是b=elo是false**

```java
import java.util.*;

public class FindAnagrams {
    public static void main(String[] args)
    {
        String s = "cbaebabacd";
        String p = "abc";
        FindAnagrams find = new FindAnagrams();
        System.out.println(find.findAnagrams(s, p));
    }

    public String findAnagrams(String s, String p)
    {
        ArrayList<Integer> result = new ArrayList<>();

        Map mapS = new HashMap();
        Map mapP = new HashMap();
        int lenP = p.length();
        for(int i = 0; i < lenP; i++) {
            char keyS = s.charAt(i);
            if(mapS.containsKey(keyS))
                mapS.put(keyS, (int)mapS.get(keyS)+1);
            else
                mapS.put(keyS, 1);

            char keyP = p.charAt(i);
            if(mapP.containsKey(keyP))
                mapP.put(keyP, (int)mapP.get(keyP)+1);
            else
                mapP.put(keyP, 1);
        }

        if(mapP.equals(mapS))
            result.add(0);

        int lenS = s.length();
        for(int i = lenP; i < lenS; i++)
        {
            char keyRemove = s.charAt(i - lenP);
            if((int)mapS.get(keyRemove) == 1)
                mapS.remove(keyRemove);
            else
                mapS.put(keyRemove, (int)mapS.get(keyRemove) - 1);

            char keyAdd = s.charAt(i);
            if(mapS.containsKey(keyAdd))
                mapS.put(keyAdd, (int)mapS.get(keyAdd) + 1);
            else
                mapS.put(keyAdd, 1);

            if(mapS.equals(mapP))
                result.add(i - lenP + 1);
        }
        return result.toString();
    }
}
```

## 4 匹配

## 5 动态规划

## 6 搜索