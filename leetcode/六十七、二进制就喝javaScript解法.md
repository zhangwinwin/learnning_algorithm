## 二进制求和

思路：将两个字符串较短的用0补齐，使得两个字符串长度一致，然后从末尾进行遍历计算，得到最终结果
但由于字符串操作原因，不确定最后的结果是否会多出一位进位，所以有两种处理方式：
第一种，在进行计算时直接拼接字符串，会得到一个反向字符，需要最后再进行翻转。
第二种，按照位置给结果字符赋值，最后如果有进位，则在前方进行字符串拼接添加进位

```
/**
 * @param {string} a
 * @param {string} b
 * @return {string}
 */
var addBinary = function(a, b) {
    let ans = '';
    let res = 0;
    for (let i = a.length - 1, j = b.length - 1; i >= 0 || j >= 0; i--, j--) {
        let sum = res;
        sum += i >= 0 ? parseInt(a[i]) : 0;
        sum += j >= 0 ? parseInt(b[j]) : 0;
        ans += sum % 2;
        res = (sum / 2) >>> 0;
    }
    ans += res == 1 ? res : '';
    return ans.split('').reverse().join('')
};
```