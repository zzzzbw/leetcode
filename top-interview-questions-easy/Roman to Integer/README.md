# Roman to Integer

## 原题

[Roman to Integer](https://leetcode.com/explore/interview/card/top-interview-questions-easy/102/math/878/)

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

**Example 1:**

```
Input: "III"
Output: 3
```

**Example 2:**

```
Input: "IV"
Output: 4
```

**Example 3:**

```
Input: "IX"
Output: 9
```

**Example 4:**

```
Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

**Example 5:**

```
Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

## 解题

题目的意思就是将罗马规则的数字转为正常十进制。规则为I=1,V=5,X=10,L=50,C=100,D=500,M=1000。另外罗马字符从左到右是从大到小的规则的，假如左边比右边的小，那么就要减去右边的。这就出现了另外的几种规则即IV=4,IX=9,XL=40,XC=90,CD=400,CM=900。

### 方法1

这个方法就是根据罗马的规则直接的判断每个字符，先判断一定加上的字符，如V则加5,L则加10，然后判断有变数的，如I，有可能是加1也有可能配合后面的V是加4。解题的时候注意判断cs[i+1]的时候数组越界问题就行了。

```java
public int romanToInt(String s) {
    int i = 0;
    int count = 0;
    char[] cs = s.toCharArray();
    while (i < cs.length) {
        if (cs[i] == 'M') {
            count += 1000;
        } else if (cs[i] == 'D') {
            count += 500;
        } else if (cs[i] == 'L') {
            count += 50;
        } else if (cs[i] == 'V') {
            count += 5;
        } else if (cs[i] == 'C') {
            if (i < cs.length - 1 && cs[i + 1] == 'D') {
                count += 400;
                i++;
            } else if (i < cs.length - 1 && cs[i + 1] == 'M') {
                count += 900;
                i++;
            } else {
                count += 100;
            }
        } else if (cs[i] == 'X') {
            if (i < cs.length - 1 && cs[i + 1] == 'L') {
                count += 40;
                i++;
            } else if (i < cs.length - 1 && cs[i + 1] == 'C') {
                count += 90;
                i++;
            } else {
                count += 10;
            }
        } else if (cs[i] == 'I') {
            if (i < cs.length - 1 && cs[i + 1] == 'V') {
                count += 4;
                i++;
            } else if (i < cs.length - 1 && cs[i + 1] == 'X') {
                count += 9;
                i++;
            } else {
                count += 1;
            }
        }
        i++;
    }
    return count;
}
```

### 方法2

这个方法就是根据罗马数字的规则来，从左到右是大到小的规则，如果左边比右边的小，那么此时就不是加这个数而是减去这个数。

```java
private static final Map<Character, Integer> romanMap = new HashMap<>(8);
static {
    romanMap.put('I', 1);
    romanMap.put('V', 5);
    romanMap.put('X', 10);
    romanMap.put('L', 50);
    romanMap.put('C', 100);
    romanMap.put('D', 500);
    romanMap.put('M', 1000);
}

public int romanToInt(String s) {
    char[] cs = s.toCharArray();
    int count = 0;
    for (int i = 0; i < cs.length; i++) {
        if (i == cs.length - 1) {
            count += romanMap.get(cs[i]);
            break;
        }
        int temp = romanMap.get(cs[i]);
        int after = romanMap.get(cs[i + 1]);
        if (temp < after) {
            count -= temp;
        } else {
            count += temp;
        }
    }
    return count;
}
```








