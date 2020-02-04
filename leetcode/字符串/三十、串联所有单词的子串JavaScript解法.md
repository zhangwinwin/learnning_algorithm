## 串联所有单词的子串
给定一个字符串 s 和一些长度相同的单词 words。找出 s 中恰好可以由 words 中所有单词串联形成的子串的起始位置。

注意子串要与 words 中的单词完全匹配，中间不能有其他字符，但不需要考虑 words 中单词串联的顺序。

 

示例 1：

输入：
  s = "barfoothefoobarman",
  words = ["foo","bar"]
输出：[0,9]
解释：
从索引 0 和 9 开始的子串分别是 "barfoo" 和 "foobar" 。
输出的顺序不重要, [9,0] 也是有效答案。
示例 2：

输入：
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
输出：[]

### 解法步骤
首先，把所有单词存到HashMap里，key存单词，value存单词出现的个数。
然后扫描子串的单词，如果当前扫描的单词在之前的HashMap中，就把该单词存到新的HashMap中，并判断新的HashMap中该单词的value是不是大于之前的HashMap该单词的value。

每次移动一个单词的长度，可以分为三类：<br>
1、 从0开始 i=0, i=3, i=6;<br>
2、 从1开始 i=1, i=4, i=7;<br>
3、 从2开始 i=2, i=5, i=8;<br>

**优化**：<br>
1、当子串完全匹配，移动到下一个子串的时候<br>
举例：<br>
barfoofoo foobarman<br>
bar foofoofoo barman<br>
前两个foo都不用判断，从第三个foo开始<br>

2、当判断过程中，出现不符合单词<br>
barfoothe foobarman<br>
barfoothe foobarman<br>
直接判断i=9的情况<br>

3、判断过程中，出现的是最符合的单词，但次数超过了<br>
foobarfoobar barman<br>
foo barfoobarbar man<br>
foobar foobarbarman<br>
对于i=0的子串，此时判断的bar其实是在words中。但之前已经出现过一次，所以i=0的子串是不符合要求的，只需要向后移动窗口，i=3的子串foo移除，此时子串一定还有两个bar，该子串也一定不符合，再往后i=6才正常判断<br>

### 解法
执行用时 :88 ms, 在所有 javascript 提交中击败了99.61%的用户<br>
内存消耗 :41.9 MB, 在所有 javascript 提交中击败了70.45%的用户
```
/**
 * @param {string} s
 * @param {string[]} words
 * @return {number[]}
 */
var findSubstring = function(s, words) {
    let res = []
    if (!s || s.length === 0 || !words || words.length === 0) return res;
    
    let map = new Map();
    let wordLen = words[0].length;
    let wordsNum = words.length;
    for (let word of words) {
        if (map.has(word)) {
            map.set(word, map.get(word) + 1);
        } else {
            map.set(word, 1)
        }
    }
    for (let i=0; i<wordLen; i++) {
        let left=i, right=i,count=0;
        let tempMap = new Map();
        while (right + wordLen <= s.length) {
            let s1 = s.substring(right, right + wordLen);
            right += wordLen;
            if (!map.has(s1)) {
                count = 0;
                left = right;
                tempMap.clear()
            } else {
                if (tempMap.has(s1)) {
                    tempMap.set(s1, tempMap.get(s1)+1);
                } else {
                    tempMap.set(s1, 1);
                }
                count++;
                while (tempMap.get(s1) > map.get(s1)) {
                    let s2 = s.substring(left, left + wordLen);
                    left += wordLen;
                    count--;
                    if (tempMap.has(s2)) {
                        tempMap.set(s2, tempMap.get(s2)-1);
                    } else {
                        tempMap.set(s2, -1);
                    }
                }
                if (count === wordsNum) res.push(left)
            }
        }
    }
    return res
};
```