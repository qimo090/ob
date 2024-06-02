要得到一个最大的数字，可以按照以下步骤进行拼接：

1. 将数组中的数字转换为字符串。
2. 排序字符串数组，排序规则为将两个字符串拼接起来，比较大小。如果拼接后的结果字符串a+b大于b+a，则认为a大于b，反之，认为b大于a。
3. 将排序后的字符串数组按照顺序进行拼接，得到的即为最大的数字。

以下是一个示例代码（使用JavaScript）：
```js
function largestNumber(nums) {
  // 将数字转换为字符串
  let strNums = nums.map(String);
  
  // 按照拼接后的大小进行排序
  strNums.sort((a, b) => (b + a) - (a + b));
  
  // 拼接排序后的字符串数组
  let result = strNums.join('');
  
  // 处理特殊情况，如果结果以0开头，则返回'0'
  if (result.startsWith('0')) {
    return '0';
  }
  
  return result;
}

// 示例输入：[10, 2]
console.log(largestNumber([10, 2])); // 输出：210

// 示例输入：[3, 30, 34, 5, 9]
console.log(largestNumber([3, 30, 34, 5, 9])); // 输出：9534330
```

以上代码通过将数字转换为字符串，利用排序规则对字符串数组进行排序，然后按照顺序拼接字符串数组得到最大的数字。注意处理特殊情况，如果结果以0开头，则返回'0'。