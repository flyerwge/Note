# javaScript slice_slice(),splice()和split()的区别

1. slice(数组)

用法：array.slice(start,end)

解释：该方法是对数组进行部分截取，并返回一个数组副本；参数start是截取的开始数组索引，end参数等于你要取的最后一个字符的位置值加上1(可选)

2. slice(字符串)

用法：string.slice(start,end)

解释：slice方法复制string的一部分来构造一个新的字符串，用法与参数匀和数组的slice方法一样;end参数等于你要取的最后一个字符的位置值加上1。

3. splice(数组)

用法：array.splice(start,deleteCount,item...)

解释：splice方法从array中移除一个或多个数组，并用新的item替换它们。参数start是从数组array中移除元素的开始位置。参数deleteCount是要移除的元素的个数。

4. split(字符串)

用法：string.split(separator,limit)

解释：split方法把这个string分割成片段来创建一个字符串数组。可选参数limit可以限制被分割的片段数量。separator参数可以是一个字符串或一个正则表达式。

