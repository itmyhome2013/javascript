#### 2.2.3 换行


##### [强制] 每个独立语句结束后必须换行。

##### [强制] 每行不得超过 `120` 个字符。

解释：

超长的不可分割的代码允许例外，比如复杂的正则表达式。长字符串不在例外之列。


##### [强制] 运算符处换行时，运算符必须在新行的行首。

示例：

```javascript
// good
if (user.isAuthenticated()
    && user.isInRole('admin')
    && user.hasAuthority('add-admin')
    || user.hasAuthority('delete-admin')
) {
    // Code
}

var result = number1 + number2 + number3
    + number4 + number5;


// bad
if (user.isAuthenticated() &&
    user.isInRole('admin') &&
    user.hasAuthority('add-admin') ||
    user.hasAuthority('delete-admin')) {
    // Code
}

var result = number1 + number2 + number3 +
    number4 + number5;
```

##### [强制] 在函数声明、函数表达式、函数调用、对象创建、数组创建、for语句等场景中，不允许在 `,` 或 `;` 前换行。

示例：

```javascript
// good
var obj = {
    a: 1,
    b: 2,
    c: 3
};

foo(
    aVeryVeryLongArgument,
    anotherVeryLongArgument,
    callback
);


// bad
var obj = {
    a: 1
    , b: 2
    , c: 3
};

foo(
    aVeryVeryLongArgument
    , anotherVeryLongArgument
    , callback
);
```

##### [建议] 不同行为或逻辑的语句集，使用空行隔开，更易阅读。

示例：

```javascript
// 仅为按逻辑换行的示例，不代表setStyle的最优实现
function setStyle(element, property, value) {
    if (element == null) {
        return;
    }

    element.style[property] = value;
}
```

##### [建议] 在语句的行长度超过 `120` 时，根据逻辑条件合理缩进。

示例：

```javascript
// 较复杂的逻辑条件组合，将每个条件独立一行，逻辑运算符放置在行首进行分隔，或将部分逻辑按逻辑组合进行分隔。
// 建议最终将右括号 ) 与左大括号 { 放在独立一行，保证与 if 内语句块能容易视觉辨识。
if (user.isAuthenticated()
    && user.isInRole('admin')
    && user.hasAuthority('add-admin')
    || user.hasAuthority('delete-admin')
) {
    // Code
}

// 按一定长度截断字符串，并使用 + 运算符进行连接。
// 分隔字符串尽量按语义进行，如不要在一个完整的名词中间断开。
// 特别的，对于HTML片段的拼接，通过缩进，保持和HTML相同的结构。
var html = '' // 此处用一个空字符串，以便整个HTML片段都在新行严格对齐
    + '<article>'
    +     '<h1>Title here</h1>'
    +     '<p>This is a paragraph</p>'
    +     '<footer>Complete</footer>'
    + '</article>';

// 也可使用数组来进行拼接，相对 + 更容易调整缩进。
var html = [
    '<article>',
        '<h1>Title here</h1>',
        '<p>This is a paragraph</p>',
        '<footer>Complete</footer>',
    '</article>'
];
html = html.join('');

// 当参数过多时，将每个参数独立写在一行上，并将结束的右括号 ) 独立一行。
// 所有参数必须增加一个缩进。
foo(
    aVeryVeryLongArgument,
    anotherVeryLongArgument,
    callback
);

// 也可以按逻辑对参数进行组合。
// 最经典的是baidu.format函数，调用时将参数分为“模板”和“数据”两块
baidu.format(
    dateFormatTemplate,
    year, month, date, hour, minute, second
);

// 当函数调用时，如果有一个或以上参数跨越多行，应当每一个参数独立一行。
// 这通常出现在匿名函数或者对象初始化等作为参数时，如setTimeout函数等。
setTimeout(
    function () {
        alert('hello');
    },
    200
);

order.data.read(
    'id=' + me.model.id, 
    function (data) {
        me.attchToModel(data.result);
        callback();
    }, 
    300
);

// 链式调用较长时采用缩进进行调整。
$('#items')
    .find('.selected')
    .highlight()
    .end();

// 三元运算符由3部分组成，因此其换行应当根据每个部分的长度不同，形成不同的情况。
var result = thisIsAVeryVeryLongCondition
    ? resultA : resultB;

var result = condition
    ? thisIsAVeryVeryLongResult
    : resultB;

// 数组和对象初始化的混用，严格按照每个对象的 { 和结束 } 在独立一行的风格书写。
var array = [
    {
        // ...
    },
    {
        // ...
    }
];
```

##### [建议] 对于 `if...else...`、`try...catch...finally` 等语句，推荐使用在 `}` 号后添加一个换行 的风格，使代码层次结构更清晰，阅读性更好。

示例：

```javascript
if (condition) {
    // some statements;
}
else {
    // some statements;
}

try {
    // some statements;
}
catch (ex) {
    // some statements;
}
```