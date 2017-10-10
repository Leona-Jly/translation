[TOC]

# React Router v4 中文文档

### [英文原文链接](https://reacttraining.com/react-router/core/guides/philosophy)

## Guides 指南
### 理念
这篇指南的目的是为了解释使用React Router时的构思模型。我们称之为"动态路由"，与你们可能更熟悉的静态路由有相当大的区别。

#### Static Routing 静态路由
如果你用过Rails、Express、Ember、Angular等等，你肯定已经用过静态路由。这些框架在渲染之前就需要声明路由作为app初始化的一部分。React Router在v4版本之前(大部分)也是静态的。让我们看下在express框架中是如何设置路由的：

```js
app.get('/', handleIndex)
app.get('/invoices', handleInvoices)
app.get('/invoices/:id', handleInvoice)
app.get('/invoices/:id/edit', handleInvoiceEdit)

app.listen()
```

注意在app监听之前是如何声明路由的。客户端的路由都是类似的。在Angular中，提前声明好路由，然后将其引入到顶层`AppModule`中。在渲染之前：

```js
const appRoutes: Routes = [
  { path: 'crisis-center',
    component: CrisisListComponent
  },
  { path: 'hero/:id',
    component: HeroDetailComponent
  },
  { path: 'heroes',
    component: HeroListComponent,
    data: { title: 'Heroes List' }
  },
  { path: '',
    redirectTo: '/heroes',
    pathMatch: 'full'
  },
  { path: '**',
    component: PageNotFoundComponent
  }
];

@NgModule({
  imports: [
    RouterModule.forRoot(appRoutes)
  ]
})

export class AppModule { }
```

Ember提供一个传统的`routes.js`文件来读取并引入路由到程序中。这同样也是发生在app渲染之前。

```js
Router.map(function() {
  this.route('about');
  this.route('contact');
  this.route('rentals', function() {
    this.route('show', { path: '/:rental_id' });
  });
});

export default Router
```

尽管彼此API不同，但他们仍都属于"静态路由"模式。React Router在v4版本之前也同样遵循此模式。

要想学好React Router，就要忘光之前的模式！:O

#### 背景
坦白说，我们都对在React Router v2中采取的方式感到很失望。我们(Michael and Ryan)意识到自己只是又重新实现了部分的React(生命周期等)，这与React编写用户界面所用的构思模型不相符。我们觉得被API限制住了。

在准备去开应对会议之前，我们走在酒店的走廊，互相问对方: "如果用我们在研讨会上教授的模式来建立路由会怎么样呢？"

我们只花了几个小时就验证了这就是我们想要的路由。我们最后制定的API，不是独立于React"之外"，而是与React自然融合。你肯定会爱上它的。

#### Dynamic Routing 动态路由
我们说的动态路由，指的是能和app渲染同时进行的路由，而不是一项脱离app运行之外的配置或约定。这也就意味着在React Router中，几乎一切都是一个组件。60秒回顾下API是如何工作的：

- 首先，根据项目环境引入`Router`组件，在app顶部渲染。
```js
// react-native
import { NativeRouter } from 'react-router-native'

// react-dom (这里我们将用此作为案例)
import { BrowserRouter } from 'react-router-dom'

ReactDOM.render((
  <BrowserRouter>
    <App/>
  </BrowserRouter>
), el)
```

- 接下来，使用link链接组件来链接到新地址：
```js
const App = () => (
  <div>
    <nav>
      <Link to="/dashboard">Dashboard</Link>
    </nav>
  </div>
)
```

- 最后，渲染一个`Route`路由，当用户访问`/dashboard`时展示用户界面。
```js
const App = () => (
  <div>
    <nav>
      <Link to="/dashboard">Dashboard</Link>
    </nav>
    <div>
      <Route path="/dashboard" component={Dashboard}/>
    </div>
  </div>
)
```

`Route`会渲染`<Dashboard {...props}/>`，其中`props`是路由特定的一些参数，像`{ match, location, history }`。如果用户**没有**访问`/dashboard`，则`Route`会渲染`null`。就是这样，喵~

#### Nested Routes 嵌套路由
许多路由都有"嵌套路由"的概念。如果你用过React Router v4之前的版本，你应该也知道！将静态路由配置为动态后，该如何"嵌套路由"呢？想想，你都是怎么嵌套`div`的？
```js
const App = () => (
  <BrowserRouter>
    {/* 这里是个 div */}
    <div>
      {/* 这里是个路由 Route */}
      <Route path="/tacos" component={Tacos}/>
    </div>
  </BrowserRouter>
)

// 当url匹配`/tacos`时，渲染此组件
const Tacos  = ({ match }) => (
  // 这里是个嵌套的 div
  <div>
    {/* 这里是个嵌套的路由 Route
        match.url帮我们配置相关路径，这里即"/tacos" */}
    <Route
      path={match.url + '/carnitas'}
      component={Carnitas}
    />
  </div>
)
```

明白路由为什么没有"嵌套"API了吗？`Route`只是个组件，就像`div`一样。所以，想要嵌套一个`Route`或者`div`，你只要……做就行了。

来点更难的。

#### 响应式路由
思考一下，一个用户跳转到了`/invoices`发票页面。你的app能够适应不同屏幕尺寸，当屏幕窄的时候，只展示发票列表以及一个能跳转到发票展示页的链接。他们能够从那里跳转到更深层次的页面。
```
Small Screen
url: /invoices

+----------------------+
|                      |
|      Dashboard       |
|                      |
+----------------------+
|                      |
|      Invoice 01      |
|                      |
+----------------------+
|                      |
|      Invoice 02      |
|                      |
+----------------------+
|                      |
|      Invoice 03      |
|                      |
+----------------------+
|                      |
|      Invoice 04      |
|                      |
+----------------------+
```

在大屏幕上，我们会展示主从复合结构页面，左侧是导航，右侧是展示页或者特定的发票页。
```
Large Screen
url: /invoices/dashboard

+----------------------+---------------------------+
|                      |                           |
|      Dashboard       |                           |
|                      |   Unpaid:             5   |
+----------------------+                           |
|                      |   Balance:   $53,543.00   |
|      Invoice 01      |                           |
|                      |   Past Due:           2   |
+----------------------+                           |
|                      |                           |
|      Invoice 02      |                           |
|                      |   +-------------------+   |
+----------------------+   |                   |   |
|                      |   |  +    +     +     |   |
|      Invoice 03      |   |  | +  |     |     |   |
|                      |   |  | |  |  +  |  +  |   |
+----------------------+   |  | |  |  |  |  |  |   |
|                      |   +--+-+--+--+--+--+--+   |
|      Invoice 04      |                           |
|                      |                           |
+----------------------+---------------------------+
```

现在暂停一下，想想不同屏幕大小下的`/invoices`页面。在大屏幕下，它还是个有效路由吗？右侧应该放什么呢？
```js
Large Screen
url: /invoices
+----------------------+---------------------------+
|                      |                           |
|      Dashboard       |                           |
|                      |                           |
+----------------------+                           |
|                      |                           |
|      Invoice 01      |                           |
|                      |                           |
+----------------------+                           |
|                      |                           |
|      Invoice 02      |             ???           |
|                      |                           |
+----------------------+                           |
|                      |                           |
|      Invoice 03      |                           |
|                      |                           |
+----------------------+                           |
|                      |                           |
|      Invoice 04      |                           |
|                      |                           |
+----------------------+---------------------------+
```

`/invoices`在大屏幕下不是一个有效路由，但在小屏幕下却是。来点更有意思的，想象有些人有个巨大的手机。他们在竖屏时访问`/invoices`，然后旋转手机为横屏。这样，我们马上就有了足够的空间来显示主从复合结构界面，所以你应该重新设计。

React Router之前版本的静态路由似乎没有解决此问题的方法。但有了动态路由，你可以声明式地编写此功能。如果你将路由当做用户界面而非静态配置来思考，你的直觉会引导你写出如下代码：
```js
const App = () => (
  <AppLayout>
    <Route path="/invoices" component={Invoices}/>
  </AppLayout>
)

const Invoices = () => (
  <Layout>

    {/* 总是显示导航 nav */}
    <InvoicesNav/>

    <Media query={PRETTY_SMALL}>
      {screenIsSmall => screenIsSmall
        // 小屏幕不会重定向
        ? <Switch>
            <Route exact path="/invoices/dashboard" component={Dashboard}/>
            <Route path="/invoices/:id" component={Invoice}/>
          </Switch>
        // 大屏幕会重定向!
        : <Switch>
            <Route exact path="/invoices/dashboard" component={Dashboard}/>
            <Route path="/invoices/:id" component={Invoice}/>
            <Redirect from="/invoices" to="/invoices/dashboard"/>
          </Switch>
      }
    </Media>
  </Layout>
)
```

当用户将手机从竖屏旋转为横屏时，代码会自动地重定向到展示页。*路由会随用户手机的方向改变而改变。*

这只是其中一个例子。我们可以讨论的还有很多，但总结起来就是以下建议：将你们的直觉和React Router的理念保持一致，多想想组件，而不是静态路由。遇到问题时，想想如何用React的声明式组合来解决，因为几乎每个"React Router问题"都是"React问题"。

### 快速开始

### 测试

### 集成redux

### 静态路由

### 处理更新阻塞


## API
### MemoryRouter 记忆路由















