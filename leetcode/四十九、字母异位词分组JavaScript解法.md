## 字母异位词分组

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

示例:

输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]

思路：当且仅当它们的字符计数（出现的次数）相同时，两个字符串是字符异位词。
算法：将每个字符串s转换为字符数count,由26个非负整数组成，表示a,b,c的数量等。使用这些计算作为哈希映射的基础

```
let groupAnagrams = function(strs) {
    let tmp = new Array(26);
    let ans = {};
    let out = [];
    for(let i = 0;i<strs.length;i++){
        for(let k = 0;k<26;k++){
            tmp[k] = '0';
        }
        let aCode = 'a'.charCodeAt();
        let tmpI = strs[i];
        let len = tmpI.length;
        let ansKey = '';
        for(let r = 0;r<len;r++){
            tmp[tmpI[r].charCodeAt() - aCode]++;
        }
        let tmpKey = tmp.join('');
        if(ans[tmpKey]==undefined){
            ans[tmpKey] = [];
        }
        ans[tmpKey].push(tmpI)
    }
    
    for(let key in ans){
        out.push(ans[key])
    }
    return out;
};
```