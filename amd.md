#### 4.1.1 AMD


##### [强制] 使用 `AMD` 作为模块定义。

解释：

AMD 作为由社区认可的模块定义形式，提供多种重载提供灵活的使用方式，并且绝大多数优秀的 Library 都支持 AMD，适合作为规范。

目前，比较成熟的 AMD Loader 有：

- 官方实现的 [requirejs](http://requirejs.org/)
- 百度自己实现的 [esl](https://github.com/ecomfe/esl)


##### [强制] 模块 `id` 必须符合标准。

解释：

模块 id 必须符合以下约束条件：

1. 类型为 string，并且是由 `/` 分割的一系列 terms 来组成。例如：`this/is/a/module`。
2. term 应该符合 [a-zA-Z0-9_-]+ 规则。
3. 不应该有 .js 后缀。
4. 跟文件的路径保持一致。
