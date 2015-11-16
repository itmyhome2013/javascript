#### 2.4.7 类注释


##### [建议] 使用 `@class` 标记类或构造函数。

解释：

对于使用对象 `constructor` 属性来定义的构造函数，可以使用 `@constructor` 来标记。


示例：

```javascript
/**
 * 描述
 *
 * @class
 */
function Developer() {
    // constructor body
}
```

##### [建议] 使用 `@extends` 标记类的继承信息。

示例：

```javascript
/**
 * 描述
 *
 * @class
 * @extends Developer
 */
function Fronteer() {
    Developer.call(this);
    // constructor body
}
util.inherits(Fronteer, Developer);
```

##### [强制] 使用包装方式扩展类成员时， 必须通过 `@lends` 进行重新指向。

解释：

没有 `@lends` 标记将无法为该类生成包含扩展类成员的文档。


示例：

```javascript
/**
 * 类描述
 *
 * @class
 * @extends Developer
 */
function Fronteer() {
    Developer.call(this);
    // constructor body
}

util.extend(
    Fronteer.prototype,
    /** @lends Fronteer.prototype */{
        _getLevel: function () {
            // TODO
        }
    }
);
```

##### [强制] 类的属性或方法等成员信息使用 `@public` / `@protected` / `@private` 中的任意一个，指明可访问性。

解释：

生成的文档中将有可访问性的标记，避免用户直接使用非 `public` 的属性或方法。

示例：

```javascript
/**
 * 类描述
 *
 * @class
 * @extends Developer
 */
var Fronteer = function () {
    Developer.call(this);

    /**
     * 属性描述
     *
     * @type {string}
     * @private
     */
    this._level = 'T12';

    // constructor body
};
util.inherits(Fronteer, Developer);

/**
 * 方法描述
 *
 * @private
 * @return {string} 返回值描述
 */
Fronteer.prototype._getLevel = function () {
};
```