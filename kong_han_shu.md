#### 3.8.4 空函数


##### [建议] 空函数不使用 `new Function()` 的形式。

示例：

```javascript
var emptyFunction = function () {};
```

##### [建议] 对于性能有高要求的场合，建议存在一个空函数的常量，供多处使用共享。

示例：

```javascript
var EMPTY_FUNCTION = function () {};

function MyClass() {
}

MyClass.prototype.abstractMethod = EMPTY_FUNCTION;
MyClass.prototype.hooks.before = EMPTY_FUNCTION;
MyClass.prototype.hooks.after = EMPTY_FUNCTION;