英文原文：[http://emberjs.com/guides/getting-started/toggle-all-todos/](http://emberjs.com/guides/getting-started/toggle-all-todos/)

TodoMVC允许用户在已完成和未完成状态之间切换所有待办事项。它使用同一个选择框来完成该功能，当其被选中时，所有的待办事项变为已完成，相反只要有一个待办事项没有完成，其为未选中状态。

为了实现这一功能，需要修改`js/controllers/todos_controller.js`中的`allAreDone`属性，使其可以处理获取和设置行为：

```javascript
// ... additional lines truncated for brevity ...
allAreDone: function (key, value) {
  if (value === undefined) {
    return !!this.get('length') && this.everyBy('isCompleted', true);
  } else {
    this.setEach('isCompleted', value);
    this.invoke('save');
    return value;
  }
}.property('@each.isCompleted')
// ... additional lines truncated for brevity ...
```

如果没有传递`value`参数，该属性用于获取选择框当前的状态。如果`value`参数被传入，这就意味着选择框被用户操作了，我们需要设置每个待办事项的`isCompleted`属性为这个传入的值。

在模板中被使用的未完成或已完成待办事项的统计数，将会自动进行更新。

重载浏览器确保没有发生任何错误，并且上面描述的功能正常。

### 在线演示

<a class="jsbin-embed" href="http://jsbin.com/AViZATE/1/embed?live">Ember.js • TodoMVC</a><script src="http://static.jsbin.com/js/embed.js"></script>

### 附加资源

  * [用`diff`格式显示改动](https://github.com/emberjs/quickstart-code-sample/commit/47b289bb9f669edaa39abd971f5e884142988663)
  * [Ember.Checkbox API文档](/api/classes/Ember.Checkbox.html)
  * [计算属性指南](/guides/object-model/computed-properties/)
