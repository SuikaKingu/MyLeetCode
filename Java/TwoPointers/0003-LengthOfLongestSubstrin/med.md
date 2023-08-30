## 无重复字符的最长子串

### 问题描述

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

 

**示例 1:**

```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
```

### 解题

使用同向双指针同时从左向右移动，移动指针保持指针间为不重复子串，比较每次移动时的子串长度，指针移动到字符串末端结束返回最大值

```java
public int solution(String str){
			int n = str.length();
			//初始化左右指针
			int left = 0;
			int right = 1;
			int res = 0;
			//特判字符串长度不大于1时，返回字符串本身的长度
			if(n <= 1 ){
				return n;
			}
			//右指针移动到字符串末尾时结束循环
			while(right < n) {
			//substring截取的实际为left至right-1处的子串，str.charAt(right)为子串右侧最近的字符
			if(str.substring(left,right)
               .contains(str.charAt(right) + "")){
					//子串中含有右侧最近的字符时，更新左指针至子串中重复字符的位置
					//更新后的左指针和右指针间必不重复，因此右指针不动，此时子串长度减小，无需比较
					left = str.indexOf(str.charAt(right),left)+1;
				}else {
					//否则继续移动右指针，并更新子串的最长长度
					right++;
					res = Math.max(res, right-left);
				}
			}
			return res;
		}
```



### 思考

利用indexof的api获得重复字符的下标，通过比较下标代替substring+contain来判断重复

```java
public static int solution(String str) {
        int n = str.length();
        int left = 0;
        int right = 0;
        int res = 0;
        if (n <= 1) {
            return n;
        }
        while (right < n) {
			//str.charAt(right)为子串右侧最近的字符s，index为从左指针处开始从左到右第一个s的下标
            int index = str.indexOf(str.charAt(right), left);
			//s在右指针左侧说明子串中含有s
            if (index < right) {
                left = index + 1;
            } else {
                right++;
            }
            res = Math.max(res, right - left);
        }
        return res;
    }
```

