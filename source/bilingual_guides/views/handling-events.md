英文原文：[http://emberjs.com/guides/views/handling-a-view/](http://emberjs.com/guides/views/handling-a-view/)

## 处理事件 (Handling Events)

Instead of having to register event listeners on elements you'd like to
respond to, simply implement the name of the event you want to respond to
as a method on your view.

你只需简单地将想要响应事件的名字作为你的视图的方法名实现即可，而不必为响应的每个元素上注册事件监听器。

For example, imagine we have a template like this:

例如，假设我们有这样一个模板：

```handlebars
{{#view App.ClickableView}}
This is a clickable area!
{{/view}}
```

Let's implement `App.ClickableView` such that when it is
clicked, an alert is displayed:

我们这样实现`App.ClickableView`使之每当被点击，会显示一个警告框：

```javascript
App.ClickableView = Ember.View.extend({
  click: function(evt) {
    alert("ClickableView was clicked!");
  }
});
```

Events bubble up from the target view to each parent view in
succession, until the root view. These values are read-only. If you want to manually manage views in JavaScript (instead of creating them
using the `{{view}}` helper in Handlebars), see the `Ember.ContainerView`
documentation below.

事件从目标视图向父级视图逐层地冒泡直至根视图。这些值是只读的。如果你想用`JavaScript`手动管理视图（而不是通过使用`Handlebars`的`{{view}}`助手来创建它们），请查看下文`Ember.ContainerView`的说明文档。

###发送事件(Sending Events)

To have the click event from `App.ClickableView` affect the state of
your application, simply send an event to the view's controller:

为了让产生自`App.ClickableView`的事件对你的应用起到作用，很简单，向视图的控制器发送一个事件：

```javascript
App.ClickableView = Ember.View.extend({
  click: function(evt) {
    this.get('controller').send('turnItUp', 11); 
  }
});
```

If the controller has an action handler called `turnItUp`, it will be called:

如果控制器有一个叫`turnInUp`的操作处理器，它将会被调用：

```javascript
App.PlaybackController = Ember.ObjectController.extend({
  actions: {
    turnItUp: function(level){
      //Do your thing
    }
  }
});
```

If it doesn't, the message will be passed to the current route:

如果没有，这条信息将会传到当前路由：

```javascript
App.PlaybackRoute = Ember.Route.extend({
  actions: {
    turnItUp: function(level){
      //This won't be called if it's defined on App.PlaybackController
    }
  }
});
```

To see a full listing of the `Ember.View` built-in events, see the
documentation section on [Event Names](/api/classes/Ember.View.html#toc_event-names).

查看Ember文档中[事件名称](/api/classes/Ember.View.html#toc_event-names)部分，来了解所有`Ember.View`的内置事件。
