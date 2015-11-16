#### 3.10.4 delete


##### [建议] 减少 `delete` 的使用。

解释：

如果没有特别的需求，减少或避免使用`delete`。`delete`的使用会破坏部分 JavaScript 引擎的性能优化。


##### [建议] 处理 `delete` 可能产生的异常。

解释：

对于有被遍历需求，且值 null 被认为具有业务逻辑意义的值的对象，移除某个属性必须使用 delete 操作。

在严格模式或IE下使用 delete 时，不能被删除的属性会抛出异常，因此在不确定属性是否可以删除的情况下，建议添加 try-catch 块。

示例：

```javascript
try {
    delete o.x;
}
catch (deleteError) {
    o.x = null;
}
```

