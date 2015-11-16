#### 2.4.12 AMD 模块注释


##### [强制] AMD 模块使用 `@module` 或 `@exports` 标识。

解释：

@exports 与 @module 都可以用来标识模块，区别在于 @module 可以省略模块名称。而只使用 @exports 时在 namepaths 中可以省略 module: 前缀。


示例：

```javascript
define(
    function (require) {

        /**
         * foo description
         *
         * @exports Foo
         */
        var foo = {
            // TODO
        };

        /**
         * baz description
         *
         * @return {boolean} return description
         */
        foo.baz = function () {
            // TODO
        };

        return foo;

    }
);
```

也可以在 exports 变量前使用 @module 标识：

```javascript
define(
    function (require) {

        /**
         * module description.
         *
         * @module foo
         */
        var exports = {};


        /**
         * bar description
         *
         */
        exports.bar = function () {
            // TODO
        };

        return exports;
    }
);
```

如果直接使用 factory 的 exports 参数，还可以：

```javascript
/**
 * module description.
 *
 * @module
 */
define(
    function (require, exports) {

        /**
         * bar description
         *
         */
        exports.bar = function () {
            // TODO
        };
        return exports;
    }
);
```

##### [强制] 对于已使用 `@module` 标识为 AMD模块 的引用，在 `namepaths` 中必须增加 `module:` 作前缀。

解释：

namepaths 没有 module: 前缀时，生成的文档中将无法正确生成链接。

示例：

```javascript
/**
 * 点击处理
 *
 * @fires module:Select#change
 * @private
 */
Select.prototype.clickHandler = function () {
    /**
     * 值变更时触发
     *
     * @event module:Select#change
     * @param {Object} e e描述
     * @param {string} e.before before描述
     * @param {string} e.after after描述
     */
    this.fire(
        'change',
        {
            before: 'foo',
            after: 'bar'
        }
    );
};
```

##### [建议] 对于类定义的模块，可以使用 `@alias` 标识构建函数。

示例：

```javascript
/**
 * A module representing a jacket.
 * @module jacket
 */
define(
    function () {

        /**
         * @class
         * @alias module:jacket
         */
        var Jacket = function () {
        };

        return Jacket;
    }
);
```


##### [建议] 多模块定义时，可以使用 `@exports` 标识各个模块。

示例：

```javascript
// one module
define('html/utils',
    /**
     * Utility functions to ease working with DOM elements.
     * @exports html/utils
     */
    function () {
        var exports = {
        };

        return exports;
    }
);

// another module
define('tag',
    /** @exports tag */
    function () {
        var exports = {
        };

        return exports;
    }
);
```

##### [建议] 对于 exports 为 Object 的模块，可以使用`@namespace`标识。

解释：

使用 @namespace 而不是 @module 或 @exports 时，对模块的引用可以省略 module: 前缀。

##### [建议] 对于 exports 为类名的模块，使用 `@class` 和 `@exports` 标识。


示例：

```javascript

// 只使用 @class Bar 时，类方法和属性都必须增加 @name Bar#methodName 来标识，与 @exports 配合可以免除这一麻烦，并且在引用时可以省去 module: 前缀。
// 另外需要注意类名需要使用 var 定义的方式。

/**
 * Bar description
 *
 * @see foo
 * @exports  Bar
 * @class
 */
var Bar = function () {
    // TODO
};

/**
 * baz description
 *
 * @return {(string|Array)} return description
 */
Bar.prototype.baz = function () {
    // TODO
};
```