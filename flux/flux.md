```javascript
知识点
	- flux

让 view 更加专注于 `视图`
```

# flux

**Flux 是一种架构思想，专门解决软件的结构问题。它跟[MVC 架构](http://www.ruanyifeng.com/blog/2007/11/mvc.html)是同一类东西，但是更加[简单和清晰](http://www.infoq.com/news/2014/05/facebook-mvc-flux)。** 

Flux将一个应用分成四个部分。

> - **View**： 视图层
> - **Action**（动作）：视图层发出的消息（比如mouseClick）
> - **Dispatcher**（派发器）：用来接收Actions、执行回调函数
> - **Store**（数据层）：用来存放应用的状态，一旦发生变动，就提醒Views要更新页面

![flux流程图](D:\桌面\note\flux\flux流程图.png)

Flux 的最大特点，就是数据的"单向流动"。

> 1. 用户访问 View
> 2. View 发出用户的 Action
> 3. Dispatcher 收到 Action，要求 Store 进行相应的更新
> 4. Store 更新后，发出一个"change"事件
> 5. View 收到"change"事件后，更新页面

