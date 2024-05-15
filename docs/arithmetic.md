# 有趣的算法题

## 题目一：数组积水问题

给定一个数组，数值为台阶高度，不同台阶高度形成不同的凹槽。计算下雨时，凹槽能够积水的大小。

如数组：{0,1,0,2} 则1与2之间的0能够形成一个凹槽，则返回1。
数组：{1,2,1,2} 则2与2之间的1能够形成一个凹槽，则返回1。

解题思路：**将数组转为二维数组，以0、1区分是否有台阶，排除首尾台阶、无边界台阶，按层级计算积水量。**

以下是Java的解题代码：

```java
    public static void main(String[] args) {
        Hard2024510 hard2024510 = new Hard2024510();
        System.out.println(hard2024510.countWater(new int[]{0,1,0,2,1,0,1,3,2,1,2,1}));
    }

    public int countWater(int[] arrs) {
        //取出最高层数
        int max = Arrays.stream(arrs).max().getAsInt();

        //转换为2维数组
        int[][] ints = turnArrays(arrs, max);

        int total = 0;
        //按层数计算积水
        for (int i = 0; i < max; i++) {
            total += countCurrent(ints[i]);
        }
        return total;
    }

    //转换为按楼层的二维数组
    private int[][] turnArrays(int[] arrs, int max) {
        int[][] result = new int[max][arrs.length];

        for (int i = 0; i < arrs.length; i++) {
            int arr = arrs[i];
            if (arr > 0) {
                //需要二维数组置为1
                for (int i1 = 0; i1 < arr; i1++) {
                    for (int i2 = 0; i2 < max; i2++) {
                        result[i2][i] = 1;
                    }

                }
            }
        }
        return result;
    }

    //核心算法
    private int countCurrent(int[] arrs) {
        int total = 0;
        for (int i = 0; i < arrs.length; i++) {
            //首尾不算
            if (i == 0 || i == arrs.length - 1) {
                continue;
            }

            //无边界不算
            if(arrs[i] == 0){
                boolean hasLast = false;
                boolean hasEnd = false;
                for (int i1 = 0; i1 < arrs.length; i1++) {
                    if (i1 < i && arrs[i1] == 1){
                        hasLast = true;
                    }else if (i1> i && arrs[i1] == 1){
                        hasEnd = true;
                    }

                    if(hasLast && hasEnd){
                        break;
                    }
                }
                if (hasLast && hasEnd){
                    total += 1;
                }
            }
        }

        return total;
    }

```

## 题目二：无重复字符的最长子串

给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串的长度。

```
示例 1:

输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

解题思路：暴力破解 或使用 滑动窗口

```java
    //这里我用暴力破解
    private int lengthOfLongestSubstring(String s) {
        if(s.isEmpty()){
            return 0;
        }
        //原视数据
        StringBuilder sb = new StringBuilder(s);
        //记录重复字段长度
        ArrayList<Integer> lengthRe = new ArrayList<>();
        //逐个遍历 获取当前值起始到重复长度
        for (int i = 0; i < sb.length(); i++) {
            StringBuilder noRepStr = new StringBuilder();
            noRepStr.append(sb.charAt(i));

            if(i+1 == sb.length()){
                lengthRe.add(noRepStr.length());
            }else {
                for (int j = i + 1; j < sb.length(); j++) {
                    int hasRep = noRepStr.indexOf(String.valueOf(sb.charAt(j)));
                    if (hasRep != -1) {
                        //有重复 记录当前到未重复的长度
                        int length = j - i;
                        lengthRe.add(length);
                        break;
                    }

                    noRepStr.append(sb.charAt(j));

                    if (j == sb.length() - 1) {
                        //到最后都没重复，做记录
                        int length = j - i + 1;
                        lengthRe.add(length);
                    }
                }
            }
        }

        return Collections.max(lengthRe);
    }
```