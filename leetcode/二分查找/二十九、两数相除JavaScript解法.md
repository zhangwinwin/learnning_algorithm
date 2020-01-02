## 两数相除

给定两个整数，被除数 dividend 和除数 divisor。将两数相除，要求不使用乘法、除法和 mod 运算符。

返回被除数 dividend 除以除数 divisor 得到的商。

示例 1:

输入: dividend = 10, divisor = 3
输出: 3
示例 2:

输入: dividend = 7, divisor = -3
输出: -2
说明:

被除数和除数均为 32 位有符号整数。
除数不为 0。
假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。本题中，如果除法结果溢出，则返回 231 − 1。<br>

执行用时 :80 ms, 在所有 javascript 提交中击败了92.81%的用户<br>
内存消耗 :34.7 MB, 在所有 javascript 提交中击败了76.47%的用户
```
/**
 * @param {number} dividend
 * @param {number} divisor
 * @return {number}
 */
var divide = function(dividend, divisor) {
    const sign = (dividend > 0) ^ (divisor > 0);
    dividend = -Math.abs(dividend);
    divisor = -Math.abs(divisor);
    let result = 0;
    while(dividend <= divisor) {
        let temp_result = -1;
        let temp_dividor = divisor;
        while (dividend <= (temp_dividor << 1)) {
            if (temp_dividor <= (1<<31) >> 1) break;
            temp_result = temp_result << 1;
            temp_dividor = temp_dividor << 1;
        }
        dividend = dividend - temp_dividor;
        result += temp_result;
    }
    if (!sign) {
        if (result <= (1<<31)) {
            return -(1<<31) -1
        }
        result = -result;
    }
    return result;
};
```
```
/**
 * @param {number} dividend
 * @param {number} divisor
 * @return {number}
 */
var divide = function(dividend, divisor) {
    const sign = (dividend > 0) ^ (divisor > 0)
    dividend = Math.abs(dividend);
    divisor = Math.abs(divisor);
    let count = 0;
    while (dividend >= divisor) {
        count += 1;
        divisor <<= 1;
    }
    let result = 0;
    while (count > 0) {
        count -= 1;
        divisor >>= 1
        if (divisor <= dividend) {
            result += 1 << count
            dividend -= divisor
        }
    }
    if (sign) {
        result = -result;
    }
    if ((-1<<31 <= result) && (result <= -(1<<31) - 1)) {
        return result
    } else {
        return (1<<31)-1
    }
};
```