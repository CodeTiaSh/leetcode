[leetcode 03 Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

解析：最长不重复子字符串，为了保证计算的都是连续字符的长度，使用双指针法+Map进行统计，tailIndex遍历整个字符串，headIndex标记最后一个不重复字符串的开头，Map用来存储当前headIndex、tailIndex中不重复字符串。

1. 双指针+Map，时间复杂度O(n)，空间复杂度O(n) （滑动窗口）

   ```java
   public int lengthOfLongestSubstring(String s) {
       if (s == null || s.length() <= 0) {
           return 0;
       }
       int tailIndex = 0;
       int headIndex = 0;
       HashSet set = new HashSet();
       int maxLength = 0;
       while (headIndex < s.length() && tailIndex < s.length()) {
           char newValue = s.charAt(tailIndex);
           if (set.contains(newValue)) {
               char oldValue = s.charAt(headIndex);
               while (oldValue != newValue && headIndex < tailIndex) {
                   set.remove(oldValue);
                   headIndex++;
                   oldValue = s.charAt(headIndex);
               }
               //headIndex++ 相当于把headIndex对应的char移出了Map
               //tailIndex++ 相当于把tailIndex对应的char添加进了Map
               //所以两个指针都需要向后移动
               headIndex++;
               tailIndex++;
           } else {
               set.add(newValue);
               tailIndex++;
           }
           if (set.size() > maxLength) {
               maxLength = set.size();
           }
       }
       return maxLength;
   }
   ```

