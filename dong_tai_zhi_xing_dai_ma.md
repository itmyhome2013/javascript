#### 3.10.2 动态执行代码


##### [建议] 使用 `new Function` 执行动态代码。

解释：

通过 new Function 生成的函数作用域是全局使用域，不会影响当当前的本地作用域。如果有动态代码执行的需求，建议使用 new Function。


示例：

```javascript
var handler = new Function('x', 'y', 'return x + y;');
var result = handler($('#x').val(), $('#y').val());
```
