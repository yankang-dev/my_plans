5.2.12	查找众数及中位数（*）
时间限制：1秒 | 内存限制：262144K | 语言限制：不限
1.众数是指一组数据中出现次数量多的那个数，众数可以是多个
2.中位数是指把一组数据从小到大排列，最中间的那个数，如果这组数据的个数是奇数，那最中间那个就是中位数，如果这组数据的个数为偶数，那就把中间的两个数之和除以2，所得的结果就是中位数
3.查找整型数组中元素的众数并组成一个新的数组，求新数组的中位数
参数代码（Java）：
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.TreeMap;

public class Main {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
            String[] arr = br.readLine().split(" ");
            TreeMap<Integer, Integer> map = new TreeMap<Integer, Integer>();
            for (String ele : arr) {
                map.merge(Integer.valueOf(ele), 1, Integer::sum);
            }
            int max = 0;
            for (int count : map.values()) {
                if (count > max) {
                    max = count;
                }
            }
            List<Integer> nums = new ArrayList<>();
            for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
                if (max == entry.getValue()) {
                    nums.add(entry.getKey());
                }
            }
            int size = nums.size();
            if (size % 2 == 0) {
                System.out.println((nums.get(size/2) + nums.get(size/2 - 1))/2);
            } else {
                System.out.println(nums.get(size/2));
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
5.2.13	单词接龙（*）
时间限制：1秒 | 内存限制：262144K | 语言限制：C、C++、Pascal、Java、Python、Php、C#、Object C、Python 3、Javascript、Javascript_V8、Sqlite、R、Go、Ruby、Swift、Matlab、C++14、Bash、Pypy2、Pypy3
单词接龙的规则是：可用于接龙的单词首字母必须要前一个单词的尾字母相同；当存在多个首字母相同的单词时，取长度最长的单词，如果长度也相等，则取字典序最小的单词；已经参与接龙的单词不能重复使用。
现给定一组全部由小写字母组成单词数组，并指定其中的一个单词作为起始单词，进行单词接龙，请输出最长的单词串，单词串是单词拼接而成，中间没有空格。
参考代码（Java）：
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
            int startIndex = Integer.parseInt(br.readLine());
            int size = Integer.parseInt(br.readLine());
            String[] words = new String[size];
            Map<String, List<Integer>> map = new HashMap<>();
            for (int i = 0; i < size; i++) {
                words[i] = br.readLine();
                if (i == startIndex) {
                    continue;
                }
                String first = words[i].substring(0, 1);
                if (map.containsKey(first)) {
                    map.get(first).add(i);
                } else {
                    List<Integer> list = new ArrayList<>();
                    list.add(i);
                    map.put(first, list);
                }
            }
            int cur = startIndex;
            StringBuilder sb = new StringBuilder(words[cur]);
            while ((cur = getNextWord(words[cur].substring(words[cur].length()-1), map, words)) != -1) {
                sb.append(words[cur]);
            }
            System.out.println(sb.toString());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static int getNextWord(String key, Map<String, List<Integer>> wordMap, String[] words) {
        List<Integer> list = wordMap.get(key);
        if (list == null || list.isEmpty()) {
            return -1;
        }
        int length = 0;
        Integer index = -1;
        for (int in : list) {
            String word = words[in];
            if (word.length() > length) {
                length = word.length();
                index = in;
                continue;
            }
            if (word.length() == length) {
                index = words[index].compareTo(word) <= 0 ? index : in;
            }
        }
        list.remove(index);
        return index;
    }
}
5.2.14	检查是否存在满足条件的数字组合（*）
时间限制：1秒 | 内存限制：262144K | 语言限制：不限
给定一个正整数数组，检查数组中是否存在满足规则的数字组合
规则：
A = B + 2C
1 2 3 4 5 6 7
1 2 4
4 = 2 + 2 * 1
import java.util.*;

public class Main {
    public static void main(String args[]) {
        Scanner sc = new Scanner(System.in);
        int a = 0;
        int count=0 ;
        String str="";
        while (sc.hasNextLine()){
            if (a==2){
                break;
            }
            if (count==0){
                count = Integer.parseInt(sc.nextLine());
                if (count<3){
                    System.out.println(0);
                    return;
                }
            }
            str = sc.nextLine();
        }
        int[] arr = new int[count];
        String[] strAar=str.split(" ");
        for (int i=0;i<strAar.length;i++) {
            arr[i] = Integer.parseInt(strAar[i]);
        }
        Arrays.sort(arr);
        for (int i=0;i<count;i++){
            int max = arr[count-i-1];
            for (int j=0;j<count;j++){
                if (j==(count-i-1)){
                    continue;
                }
                int min = arr[j];

                for (int k=0;k<count;k++){
                    int min1 = arr[k];
                    if (j==k||k==(count-i-1)){
                        continue;
                    }

                    if (max==min+min1*2){
                        System.out.println(max + " " + min +" "+min1);
                        return;
                    }
                }
            }
        }
        System.out.println(0);
    }
}
5.2.15	字符串序列判定（*）
时间限制：3秒 | 内存限制：262144K | 语言限制：C、C++、Pascal、Java、Python、Php、C#、Object C、Python 3、Javascript、Javascript_V8、Sqlite、R、Go、Ruby、Swift、Matlab、C++14、Bash、Pypy2、Pypy3、Rust
输入两个字符串S和L，都只包含英文小写字母。S长度<=100，L长度<=500,000。判定S是否是L的有效字串。
判定规则：S中的每个字符在L中都能找到（可以不连续），且S在Ｌ中字符的前后顺序与S中顺序要保持一致。（例如，S="ace"是L="abcde"的一个子序列且有效字符是a、c、e，而"aec"不是有效子序列，且有效字符只有a、e）
5.2.16	整数对最小和（*）
时间限制：1秒 | 内存限制：262144K | 语言限制：不限
给定两个整数数组array1、array2，数组元素按升序排列。假设从array1、array2中分别取出一个元素可构成一对元素，现在需要取出k对元素，并对取出的所有元素求和，计算和的最小值
注意：两对元素如果对应于array1、array2中的两个下标均相同，则视为同一对元素。
5.2.17	找出符合要求的字符串子串（*）
时间限制：1秒 | 内存限制：262144K | 语言限制：不限
给定两个字符串，从字符串2中找出字符串1中的所有字符，去重并按照ASCII值从小到大排序
输入字符串1：长度不超过1024
输入字符串2：长度不超过1000000
字符范围满足ASCII编码要求，按照ASCII的值由小到大排序

输入描述:
bach
bbaaccedfg
输出描述:
abc
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        TreeMap<String,String> map = new TreeMap<>();
        String str1 = sc.nextLine();
        String str2 = sc.nextLine();
        char[] chars = str2.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            if (str1.contains(chars[i]+"")){
                map.put(chars[i]+"","1");
            }
        }
        for (String s : map.keySet()) {
            System.out.print(s);
        }

    }
}
5.2.18	字符串统计（*）
时间限制：1秒 | 内存限制：262144K | 语言限制：不限
给定两个字符集合，一个为全量字符集，一个为已占用字符集。已占用的字符集中的字符不能再使用，要求输出剩余可用字符集。
5.2.19	统计射击比赛成绩（*）
时间限制：1秒 | 内存限制：65536K | 语言限制：不限
给定一个射击比赛成绩单，包含多个选手若干次射击的成绩分数，请对每个选手按其最高3个分数之和进行降序排名，输出降序排名后的选手ID序列。条件如下：
1、一个选手可以有多个射击成绩的分数，且次序不固定。
2、如果一个选手成绩少于3个，则认为选手的所有成绩无效，排名忽略该选手。
3、如果选手的成绩之和相等，则成绩之和相等的选手按照其ID降序排列。
5.2.20	工号不够用了怎么办？（*）
时间限制：1秒 | 内存限制：262144K | 语言限制：不限
3020年，空间通信集团的员工人数突破20亿人，即将遇到现有工号不够用的窘境。
现在，请你负责调研新工号系统。继承历史传统，新的工号系统由小写英文字母（a-z）和数字（0-9）两部分构成。新工号由一段英文字母开头，之后跟随一段数字，比如"aaahw0001","a12345","abcd1","a00"。注意新工号不能全为字母或者数字,允许数字部分有前导0或者全为0。
但是过长的工号会增加同事们的记忆成本，现在给出新工号至少需要分配的人数X和新工号中字母的长度Y，求新工号中数字的最短长度Z。
参考代码（Java）：
import java.util.*;

public class Main {
    public static void main(String args[]) {
        Scanner sc = new Scanner(System.in);
        String str = sc.nextLine();
        long countNum = Long.parseLong(str.split(" ")[0]);
        int zimulength = Integer.parseInt(str.split(" ")[1]);
        long zimuNum =1;
        for (int i=0;i<zimulength;i++){
            zimuNum *=26;
        }
        if (zimuNum>=countNum){
            System.out.println(1);
        }
        int numCount = 1;
        while (countNum>zimuNum){
            long tem = getNUm(numCount);
            if (countNum<=tem){
                System.out.println(numCount);
                return;
            }
            if (countNum<=tem*zimuNum){
                System.out.println(numCount);
                return;
            }
            numCount++;
        }
    }

    private static long getNUm(int numCount) {
        long tt = 1;
        for (int i=0;i<numCount;i++){
            tt *=10;
        }
        return tt;
    }
}
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        Long longx = in.nextLong();
        int y = in.nextInt();
        int result = (int)Math.ceil(Math.log10(longx/Math.pow(26,y)));
        result = result == 0 ? 1 : result;
        System.out.println(result);
    }
}

