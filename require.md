#### 4.1.3 require


##### [强制] 全局运行环境中，`require` 必须以 `async require` 形式调用。

解释：

模块的加载过程是异步的，同步调用并无法保证得到正确的结果。

示例：

```javascript
// good
require(['foo'], function (foo) {
});

// bad
var foo = require('foo');
```

##### [强制] 模块定义中只允许使用 `local require`，不允许使用 `global require`。

解释：

1. 在模块定义中使用 global require，对封装性是一种破坏。
2. 在 AMD 里，global require 是可以被重命名的。并且 Loader 甚至没有全局的 require 变量，而是用 Loader 名称做为 global require。模块定义不应该依赖使用的 Loader。


##### [强制] Package在实现时，内部模块的 `require` 必须使用 `relative id`。

解释：

对于任何可能通过 发布-引入 的形式复用的第三方库、框架、包，开发者所定义的名称不代表使用者使用的名称。因此不要基于任何名称的假设。在实现源码中，require 自身的其它模块时使用 relative id。

示例：

```javascript
define(
    function (require) {
        var util = require('./util');
    }
);
```


##### [建议] 不会被调用的依赖模块，在 `factory` 开始处统一 `require`。

解释：

有些模块是依赖的模块，但不会在模块实现中被直接调用，最为典型的是 css / js / tpl 等 Plugin 所引入的外部内容。此类内容建议放在模块定义最开始处统一引用。

示例：

```javascript
define(
    function (require) {
        require('css!foo.css');
        require('tpl!bar.tpl.html');

        // ...
    }
);
```
