---
permalink: /algorithm/kmp/
---

# Java KMP算法

### 算法说明后续补充

### 示例

```java
/**
 * KMP算法
 * 适合字符串模式匹配
 */
public class KMPAlgorithm {
    public static void main(String[] args) {
        String source = "BBC ABCDAB ABCDABCDABDE";
        String pattern = "ABCDABD";
        System.out.println(kmp(source, pattern));
    }

    /**
     * kmp 算法
     *
     * @param source  匹配源
     * @param pattern 匹配模式
     * @return 若匹配，返回在匹配源中的索引位置，反之返回-1
     */
    private static int kmp(String source, String pattern) {
        if (pattern.length() <= 0) {
            throw new IllegalArgumentException("匹配模式长度小于0");
        }
        int[] matchTable = calMatchTable(pattern);
        char[] sChars = source.toCharArray();
        char[] pChars = pattern.toCharArray();
        int i = 0, j = 0, moveCount = 0, matchCharCount = 0;
        while (i < sChars.length) {
            if (sChars[i] == pChars[j]) {
                matchCharCount++;
                i++;
                j++;
            } else if (j == 0) {
                i++;
            } else {
                moveCount = matchCharCount - matchTable[j - 1];
                j = j - moveCount;
                matchCharCount = matchCharCount - moveCount;
            }
            if (j == pChars.length) {
                return i - j;
            }
        }
        return -1;
    }

    /**
     * 部分匹配表
     * ABCDCABC
     * 00000123
     *
     * @param string string
     * @return 部分匹配表
     */
    private static int[] calMatchTable(String string) {
        int len = string.length();
        int[] matchTable = new int[len];
        for (int i = 0; i < len; i++) {
            int matchValue = i == 0
                    ? 0
                    : calMatchValue(string.substring(0, i + 1));
            matchTable[i] = matchValue;
        }
        return matchTable;
    }

    /**
     * 部分匹配值
     * 一个字符串的前缀字符串和后缀字符串的最大共有长度
     * ABCDCABC
     * 3 （ABC）
     *
     * @param string string
     * @return 最大共有长度
     */
    private static int calMatchValue(String string) {
        int len = string.length();
        String prefixStr = string.substring(0, len - 1);
        String suffixStr = string.substring(1);
        while (prefixStr.length() > 0 && suffixStr.length() > 0) {
            if (prefixStr.equals(suffixStr)) {
                return prefixStr.length();
            }
            if (prefixStr.length() == 1 && suffixStr.length() == 1) {
                break;
            }
            prefixStr = prefixStr.substring(0, prefixStr.length() - 1);
            suffixStr = suffixStr.substring(1);
        }
        return 0;
    }
}
```

