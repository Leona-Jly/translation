[TOC]

# React Router v4 中文文档

### [英文原文链接](https://reacttraining.com/react-router/web/guides/philosophy)

# WEB
## Guides 指南
### 理念
这篇指南的目的是为了解释使用React Router时的心智模型。我们称之为"动态路由"，与你们可能更熟悉的静态路由有相当大的区别。

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

```jsx
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

```jsx
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
坦白说，我们都对在React Router v2中采取的方式感到很失望。我们(Michael and Ryan)意识到自己只是又重新实现了部分的React(生命周期等)，这与React编写UI所用的心智模型不相符。我们觉得被API限制住了。

在准备去开应对会议之前，我们走在酒店的走廊，互相问对方: "如果用我们在研讨会上教授的模式来建立路由会怎么样呢？"

我们只花了几个小时就验证了这就是我们想要的路由。我们最后制定的API，不是独立于React"之外"，而是与React自然融合。你肯定会爱上它的。

#### Dynamic Routing 动态路由
我们说的动态路由，指的是能和app渲染同时进行的路由，而不是一项脱离app运行之外的配置或约定。这也就意味着在React Router中，几乎一切都是一个组件。60秒回顾下API是如何工作的：

首先，根据项目环境引入`Router`组件，在app顶部渲染。
```jsx
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

接下来，使用link链接组件来链接到新地址：
```jsx
const App = () => (
  <div>
    <nav>
      <Link to="/dashboard">Dashboard</Link>
    </nav>
  </div>
)
```

最后，渲染一个`Route`路由，当用户访问`/dashboard`时展示UI视图。
```jsx
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

`Route`会渲染`<Dashboard {...props}/>`，其中`props`是路由特定的一些属性，像`{ match, location, history }`。如果用户**没有**访问`/dashboard`，则`Route`会渲染`null`。就是这样，喵~

#### Nested Routes 嵌套路由
许多路由都有"嵌套路由"的概念。如果你用过React Router v4之前的版本，你应该也知道！将静态路由配置为动态后，该如何"嵌套路由"呢？想想，你都是怎么嵌套`div`的？
```jsx
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
思考一下，一个用户跳转到了`/invoices`发票视图。你的app能够适应不同屏幕尺寸，当屏幕窄的时候，只展示发票列表以及一个能跳转到发票展示页的链接。他们能够从那里跳转到更深层次的视图。
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

在大屏幕上，我们会展示主从复合结构视图，左侧是导航，右侧是展示页或者特定的发票页。
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

现在暂停一下，想想不同屏幕大小下的`/invoices`视图。在大屏幕下，它还是个有效路由吗？右侧应该放什么呢？
```jsx
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

React Router之前版本的静态路由似乎没有解决此问题的方法。但有了动态路由，你可以声明式地编写此功能。如果你将路由当做UI视图而非静态配置来思考，你的直觉会引导你写出如下代码：
```jsx
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

这只是其中一个例子。我们可以讨论的还有很多，但总结起来就是以下建议：将你们的直觉和React Router的理念保持一致，多想想组件，而不是静态路由。遇到问题时，想想如何用React的声明式可组合性来解决，因为几乎每个"React Router问题"都是"React问题"。

### 快速开始
开始一个React web项目最简单的方法就是使用Facebook开发的[Create React App](https://github.com/facebookincubator/create-react-app)工具，其拥有大量的社区帮助。

首先，若没有create-react-app则先安装，然后用其生成一个新项目。
```
npm install -g create-react-app
create-react-app demo-app
cd demo-app
```

#### 安装
[React Router DOM](https://npm.im/react-router-dom)已经发布到npm，你可以用`npm`或者`yarn`进行安装。Create React App用的是yarn，所以我们在此也用yarn。
```
yarn add react-router-dom
# 或者，如果你用的不是yarn
npm install react-router-dom
```

现在你可以复制黏贴任何一个示例代码到`src/App.js`中了。这里是个基础例子：
```jsx
import React from 'react'
import {
  BrowserRouter as Router,
  Route,
  Link
} from 'react-router-dom'

const Home = () => (
  <div>
    <h2>Home</h2>
  </div>
)

const About = () => (
  <div>
    <h2>About</h2>
  </div>
)

const Topic = ({ match }) => (
  <div>
    <h3>{match.params.topicId}</h3>
  </div>
)

const Topics = ({ match }) => (
  <div>
    <h2>Topics</h2>
    <ul>
      <li>
        <Link to={`${match.url}/rendering`}>
          Rendering with React
        </Link>
      </li>
      <li>
        <Link to={`${match.url}/components`}>
          Components
        </Link>
      </li>
      <li>
        <Link to={`${match.url}/props-v-state`}>
          Props v. State
        </Link>
      </li>
    </ul>

    <Route path={`${match.url}/:topicId`} component={Topic}/>
    <Route exact path={match.url} render={() => (
      <h3>Please select a topic.</h3>
    )}/>
  </div>
)

const BasicExample = () => (
  <Router>
    <div>
      <ul>
        <li><Link to="/">Home</Link></li>
        <li><Link to="/about">About</Link></li>
        <li><Link to="/topics">Topics</Link></li>
      </ul>

      <hr/>

      <Route exact path="/" component={Home}/>
      <Route path="/about" component={About}/>
      <Route path="/topics" component={Topics}/>
    </div>
  </Router>
)
export default BasicExample
```

现在你可以开始探索了。旅途快乐！

### 服务端渲染
因为服务器端是无状态的，所以与客户端渲染起来有些不同。基本思路就是用无状态的StaticRouter[<StaticRouter>](#StaticRouter)代替BrowserRouter[<BrowserRouter>](#BrowserRouter)来包装app，并且传入两个属性值。一个属性是服务端返回的url，这样就能匹配路由；另一个属性是`context`，我们之后会讨论。
```jsx
// 客户端
<BrowserRouter>
  <App/>
</BrowserRouter>

// 服务端(非完整版)
<StaticRouter
  location={req.url}
  context={context}
>
  <App/>
</StaticRouter>
```

在客户端渲染Redirect[<Redirect>](#Redirect)时，浏览器历史改变了app状态，展现出新视图。然而在静态服务端环境中，app状态无法被改变。所以，我们需要`context`属性来判断渲染结果。若存在`context.url`，则表示app已重定向。这样我们就能实现服务端重定向。
```jsx
const context = {}
const markup = ReactDOMServer.renderToString(
  <StaticRouter
    location={req.url}
    context={context}
  >
    <App/>
  </StaticRouter>
)

if (context.url) {
  // 某处渲染了重定向`<Redirect>`
  redirect(301, context.url)
} else {
  // 一切安好，发送response
}
```

#### 添加app特定上下文信息
路由永远只会添加`context.url`这个属性。若想要某些重定向时发送301响应，其他为302，或者想要在某些特定的UI被渲染时发送404响应，又或者想要在未认证时发送401，都可以通过改变上下文属性context来实现。下面是个区别301和302重定向的示例：
```jsx
const RedirectWithStatus = ({ from, to, status }) => (
  <Route render={({ staticContext }) => {
    // 客户端没有静态上下文`staticContext`属性，所以需在此防一下
    if (staticContext)
      staticContext.status = status
    return <Redirect from={from} to={to}/>
  }}/>
)

// app客户端
const App = () => (
  <Switch>
    {/* 其他路由 */}
    <RedirectWithStatus
      status={301}
      from="/users"
      to="/profiles"
    />
    <RedirectWithStatus
      status={302}
      from="/courses"
      to="/dashboard"
    />
  </Switch>
)

// 服务端
const context = {}

const markup = ReactDOMServer.renderToString(
  <StaticRouter context={context}>
    <App/>
  </StaticRouter>
)

if (context.url) {
  // 可在此处用RedirectWithStatus中添加的`context.status`
  redirect(context.status, context.url)
}
```

#### 404、401或其他状态
同上。创建一个组件添加上下文属性，然后在app中不同的地方渲染得到不同的状态码。
```jsx
const Status = ({ code, children }) => (
  <Route render={({ staticContext }) => {
    if (staticContext)
      staticContext.status = code
    return children
  }}/>
)
```

现在你可以在app任何一个你想要添加状态码到`staticContext`的地方渲染`Status`组件。
```jsx
const NotFound = () => (
  <Status code={404}>
    <div>
      <h1>Sorry, can’t find that.</h1>
    </div>
  </Status>
)

// 其他地方
<Switch>
  <Route path="/about" component={About}/>
  <Route path="/dashboard" component={Dashboard}/>
  <Route component={NotFound}/>
</Switch>
```

#### 汇总
这并不是一个真正的app，但是它展示了所有你需要放在一起的通用代码。
```jsx
import { createServer } from 'http'
import React from 'react'
import ReactDOMServer from 'react-dom/server'
import { StaticRouter } from 'react-router'
import App from './App'

createServer((req, res) => {
  const context = {}

  const html = ReactDOMServer.renderToString(
    <StaticRouter
      location={req.url}
      context={context}
    >
      <App/>
    </StaticRouter>
  )

  if (context.url) {
    res.writeHead(301, {
      Location: context.url
    })
    res.end()
  } else {
    res.write(`
      <!doctype html>
      <div id="app">${html}</div>
    `)
    res.end()
  }
}).listen(3000)
```

接下来是客户端：
```jsx
import ReactDOM from 'react-dom'
import { BrowserRouter } from 'react-router-dom'
import App from './App'

ReactDOM.render((
  <BrowserRouter>
    <App/>
  </BrowserRouter>
), document.getElementById('app'))
```

#### 数据加载
加载数据有无数种方式，且没有定论哪种是最佳实践，所以我们兼容所有方法，没有任何偏向。我们有信心路由能高度符合你的项目要求。

最基本的要求是在渲染前加载数据。React Router提供了`matchPath`静态函数来匹配路由。在服务端使用此函数可以在渲染前判断需要用到哪个数据。

此方法的要点是要配置好静态路由，这样既能渲染路由视图，又能判断渲染前的数据依赖。

```jsx
const routes = [
  { path: '/',
    component: Root,
    loadData: () => getSomeData(),
  },
  // 等等
]
```

配置好后使用此路由渲染app视图：
```jsx
import { routes } from './routes'

const App = () => (
  <Switch>
    {routes.map(route => (
      <Route {...route}/>
    ))}
  </Switch>
)
```

服务端写法：
```jsx
import { matchPath } from 'react-router-dom'

// 请求内部
const promises = []
// 使用`some`方法来模拟`<Switch>`的行为，只挑选出首个匹配的值
routes.some(route => {
  // 在这里使用`matchPath`
  const match = matchPath(req.url, route)
  if (match)
    promises.push(route.loadData(match))
  return match
})

Promise.all(promises).then(data => {
  // 处理data数据，以便于客户端渲染app
})
```

最后，客户端接受数据。再次说明，我们没有硬性规定数据加载模式，但这些都是实现要点。

[React Router Config](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-config)安装包提供了静态路由配置，来协助数据加载以及服务端渲染。若有兴趣，[请点此](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-config)。

### 代码拆分
web应用有一个很大的特点是用户无需下载完整即可使用。你可以把代码拆分看做是应用的按需加载(增量加载)。代码拆分工具有很多，这里我们使用[Webpack](https://webpack.github.io/)的[bundle loader](https://github.com/webpack-contrib/bundle-loader)。

我们可以通过使用`<Bundle>`来分离代码。需要着重注意的是，路由和代码分离实际上并没有什么关联。"进入某路由"仅代表"正在渲染某组件"。所以当用户进入路由时，我们提供一个能动态引入代码的组件就行了。此方法在app任意地方都适用：
```jsx
import loadSomething from 'bundle-loader?lazy!./Something'

<Bundle load={loadSomething}>
  {(mod) => (
    // 处理mod模块
  )}
</Bundle>
```

若模块为组件，则可进行渲染：
```jsx
<Bundle load={loadSomething}>
  {(Comp) => (Comp
    ? <Comp/>
    : <Loading/>
  )}
</Bundle>
```

`Bundle`组件接收一个`load`属性，属性值为webpack的[bundle loader](https://github.com/webpack-contrib/bundle-loader)中引入的值。稍后会解释为何使用它。组件在挂载或者接收新的`load`属性值时会调用`load`，并将其返回值放入state中，最后在render中使用模块进行渲染。
```jsx
// 接上例
import React, { Component } from 'react'

class Bundle extends Component {
  state = {
    // "module"是js关键字，故用简称"mod"
    mod: null
  }

  componentWillMount() {
    this.load(this.props)
  }

  componentWillReceiveProps(nextProps) {
    if (nextProps.load !== this.props.load) {
      this.load(nextProps)
    }
  }

  load(props) {
    this.setState({
      mod: null
    })
    props.load((mod) => {
      this.setState({
        // 对es imports以及commonJS进行处理
        mod: mod.default ? mod.default : mod
      })
    })
  }

  render() {
    return this.state.mod ? this.props.children(this.state.mod) : null
  }
}

export default Bundle
```

`render`在模块加载出来之前，得到的`state.mod`都是null。这点非常重要，因为能暗示用户我们需要等待某件事情。

**为什么使用bundle loader，而不是`import()`？**

我们已经使用bundle loader[多年了](https://github.com/ReactTraining/react-router/blob/9f43019b26ad625ce4673e6abf5aa0093d7a7ef4/package.json#L17)，并且在TC39继续推出官方动态引入(dynamic import)后仍在使用(? We’ve been using it for years and it continues to work while TC39 continues to come up with an official dynamic import.)。最新的提案是[import()](https://github.com/tc39/proposal-dynamic-import)，我们可以将`Bundle`组件改为使用`import()`的写法：
```jsx
<Bundle load={() => import('./something')}>
  {(mod) => ()}
</Bundle>
```

另一个使用bundle loader的巨大好处是，它的第二次回调是同步的，这样每次访问一个代码拆分视图时就不会出现加载页的闪动。

不管用何种方式进行引入，理念是一样的：组件在渲染时会处理代码的加载(? a component that handles the code loading when it renders)。现在你所要做的就是在需要动态加载代码的地方渲染`<Bundle>`组件。


#### 渲染完成后加载
`Bundle`组件不仅有助于进入新视图时的加载，也有助于在后台预加载app的其余部分。
```jsx
import loadAbout from 'bundle-loader?lazy!./loadAbout'
import loadDashboard from 'bundle-loader?lazy!./loadDashboard'

// 组件在初始化时加载他们对应的模块
const About = (props) => (
  <Bundle load={loadAbout}>
    {(About) => <About {...props}/>}
  </Bundle>
)

const Dashboard = (props) => (
  <Bundle load={loadDashboard}>
    {(Dashboard) => <Dashboard {...props}/>}
  </Bundle>
)

class App extends React.Component {
  componentDidMount() {
    // 预加载其余的
    loadAbout(() => {})
    loadDashboard(() => {})
  }

  render() {
    return (
      <div>
        <h1>Welcome!</h1>
        <Route path="/about" component={About}/>
        <Route path="/dashboard" component={Dashboard}/>
      </div>
    )
  }
}
```

app何时加载以及加载多少，由你自己而非某些特定路由决定。也许你想在用户非活跃状态时加载，也许在用户访问一个特定路由时加载，也许你想在初始化渲染后就预加载app其余部分：
```jsx
ReactDOM.render(<App/>, preloadTheRestOfTheApp)
```

#### 代码拆分 + 服务端渲染
我们尝试了几次，也失败了几次，得到了以下经验：
  1. 须在服务端同步解析模块，才能在初始渲染时就拿到模块(? bundles)。
  2. 客户端在渲染之前就要加载所有服务端所涉及渲染的模块，这样才能保持客户端与服务端的统一。(最难的部分，我觉得是可以做到的，但我选择放弃。)
  3. app其余部分使用异步的解决方法。

因为我们的网站在没有服务端渲染的情况下，也能在谷歌搜索中有不错的排名，所以我们使用了代码拆分 + service worker缓存的技术来代替之。祝那些使用服务端渲染及代码拆分的app成功。

### 滚动复位
React Router在早些版本中提供了开箱即用的滚动复位。自那以后，你们对于此功能的呼声非常高。希望这篇文档能帮你们了解到滚动和路由之间的关联和知识。

浏览器开始用`history.pushState`方法处理滚动复位，和其处理普通导航的方式一样。chrome中已生效，且效果很不错。[滚动复位规范点此链接](https://majido.github.io/scroll-restoration-proposal/history-based-api.html#web-idl)。

因为浏览器开始"默认处理滚动"，而app有着各种各样的滚动需求(比如此网站，指[英文官网](https://reacttraining.com/react-router/web/guides/scroll-restoration))，所以我们不推荐默认的滚动处理。这篇指南应该能满足你们所有的滚动需求。

#### 滚动到顶部
通常我们都会有个很长的页面且进入页面时总是会留在之前滚动的位置，所以大部分的需求都是"滚动到顶部"。我们直接构建一个`<ScrollToTop>`组件，让页面每次跳转都会滚动到顶部，记得确保外层用`withRouter`包住以便于获取路由属性：
```jsx
class ScrollToTop extends Component {
  componentDidUpdate(prevProps) {
    if (this.props.location !== prevProps.location) {
      window.scrollTo(0, 0)
    }
  }

  render() {
    return this.props.children
  }
}

export default withRouter(ScrollToTop)
```

然后在app外层、Router内层进行渲染
```jsx
const App = () => (
  <Router>
    <ScrollToTop>
      <App/>
    </ScrollToTop>
  </Router>
)

// 或者单独放在任意位置，但不能重复放 :)
<ScrollToTop/>
```

若路由切换改变的是tab标签组件，通常不需要在切换tab时滚动到顶部，则可以构建一个`<ScrollToTopOnMount>`组件放在需要的地方：
```jsx
class ScrollToTopOnMount extends Component {
  componentDidMount(prevProps) {
    window.scrollTo(0, 0)
  }

  render() {
    return null
  }
}

class LongContent extends Component {
  render() {
    <div>
      <ScrollToTopOnMount/>
      <h1>Here is my long content page</h1>
    </div>
  }
}

// 其他地方
<Route path="/long-content" component={LongContent}/>
```

#### 通用方案
我们所说的通用方法(浏览器开始内置处理机制)是指：
  1. 导航跳转新页面时滚动到顶部而非停留在底部
  2. 点击"返回"和"前进"(不是Link链接按钮)时存住滚动位置以及页面所有溢出(overflow)的元素
当时，我们也想着弄个通用API出来。以下是我们当时想的：
```jsx
<Router>
  <ScrollRestoration>
    <div>
      <h1>App</h1>

      <RestoredScroll id="bunny">
        <div style={{ height: '200px', overflow: 'auto' }}>
          I will overflow
        </div>
      </RestoredScroll>
    </div>
  </ScrollRestoration>
</Router>
```

首先，`ScrollRestoration`组件在导航到新页面时会将window滚动到顶部。其次，它会利用`location.key`来将window滚动位置*以及*`RestoredScroll`组件滚动位置存入`sessionStorage`中。然后，当`ScrollRestoration`或者`RestoredScroll`组件进行挂载时，它们可以从`sessionStorage`中获取滚动位置信息。

对我来说难的是如何定义一个在我不需要window滚动被控制时会"自愿退出"的API。举个例子，如果你页面上浮动(float)着几个tab导航时，你往往不想要滚动到顶部(tab导航可能被滚出视口)。

当我了解到chrome现在提供了滚动处理，而且你们不同app的滚动需求不尽相同时，我觉得我们没有必要再提供滚动功能了，特别是需求往往只是想要滚动到顶部而已(你自己直接写进app里就行了(? which you saw is straight-forward to add to your app on your own))。

基于此，我们不再觉得我们需要提供滚动(我们跟你们一样时间有限)。但是，我们很乐意帮你们实现一个通用方案，一个甚至能在项目中富有生命的强健方案(? A solid solution could even live in the project.)。如果你开始动手了，联系我们吧 :)

### 测试
React Router依赖于React。这影响到你们的组件测试方式，因为你们的React组件使用了我们React Router的组件。(? React Router relies on React context to work. This affects how you can test your components that use our components.)

#### 上下文
如果你想要对那些渲染出`<Link>`或者`<Route>`等的组件进行单元测试，你会得到一些关于上下文的错误和警告。你可能想要自己想办法解决路由上下文问题，但我们建议你将单元测试包裹在`<StaticRouter>`或者`<MemoryRouter>`里。看这里：
```jsx
class Sidebar extends Component {
  // ...
  render() {
    return (
      <div>
        <button onClick={this.toggleExpand}>
          expand
        </button>
        <ul>
          {users.map(user => (
            <li>
               <Link to={user.path}>
                 {user.name}
               </Link>
            </li>
          ))}
        </ul>
      </div>
    )
  }
}

// 出问题了
test('it expands when the button is clicked', () => {
  render(
    <Sidebar/>
  )
  click(theButton)
  expect(theThingToBeOpen)
})

// 解决了！
test('it expands when the button is clicked', () => {
  render(
    <MemoryRouter>
      <Sidebar/>
    </MemoryRouter>
  )
  click(theButton)
  expect(theThingToBeOpen)
})
```
就是这样。

#### 从特定路由开始
`<MemoryRouter`支持传入`initialEntries`和`initialIndex`属性，所以你可以让app(或者app的任意一部分)从一个特定路由启动。
```jsx
test('current user is active in sidebar', () => {
  render(
    <MemoryRouter initialEntries={[ '/users/2' ]}>
      <Sidebar/>
    </MemoryRouter>
  )
  expectUserToBeActive(2)
})
```

#### 导航
路由在地址(location)改变后仍有效，对此我们已经测试过多遍，所以你无须再测。若必须再测，我们可以耍点小聪明，因为一切都是在渲染(render)中发生的：
```jsx
import { render, unmountComponentAtNode } from 'react-dom'
import React from 'react'
import { Route, Link, MemoryRouter } from 'react-router-dom'
import { Simulate } from 'react-addons-test-utils'

// a way to render any part of your app inside a MemoryRouter
// you pass it a list of steps to execute when the location
// changes, it will call back to you with stuff like
// `match` and `location`, and `history` so you can control
// the flow and make assertions.
const renderTestSequence = ({
  initialEntries,
  initialIndex,
  subject: Subject,
  steps
}) => {
  const div = document.createElement('div')

  class Assert extends React.Component {

    componentDidMount() {
      this.assert()
    }

    componentDidUpdate() {
      this.assert()
    }

    assert() {
      const nextStep = steps.shift()
      if (nextStep) {
        nextStep({ ...this.props, div })
      } else {
        unmountComponentAtNode(div)
      }
    }

    render() {
      return this.props.children
    }
  }

  class Test extends React.Component {
    render() {
      return (
        <MemoryRouter
          initialIndex={initialIndex}
          initialEntries={initialEntries}
        >
          <Route render={(props) => (
            <Assert {...props}>
              <Subject/>
            </Assert>
          )}/>
        </MemoryRouter>
      )
    }
  }

  render(<Test/>, div)
}

// our Subject, the App, but you can test any sub
// section of your app too
const App = () => (
  <div>
    <Route exact path="/" render={() => (
      <div>
        <h1>Welcome</h1>
      </div>
    )}/>
    <Route path="/dashboard" render={() => (
      <div>
        <h1>Dashboard</h1>
        <Link to="/" id="click-me">Home</Link>
      </div>
    )}/>
  </div>
)

// the actual test!
it('navigates around', (done) => {

  renderTestSequence({

    // tell it the subject you're testing
    subject: App,

    // and the steps to execute each time the location changes
    steps: [

      // initial render
      ({ history, div }) => {
        // assert the screen says what we think it should
        console.assert(div.innerHTML.match(/Welcome/))

        // now we can imperatively navigate as the test
        history.push('/dashboard')
      },

      // second render from new location
      ({ div }) => {
        console.assert(div.innerHTML.match(/Dashboard/))

        // or we can simulate clicks on Links instead of
        // using history.push
        Simulate.click(div.querySelector('#click-me'), {
          button: 0
        })
      },

      // final render
      ({ location }) => {
        console.assert(location.pathname === '/')
        // you'll want something like `done()` so your test
        // fails if you never make it here.
        done()
      }
    ]
  })
})
```





















### 集成redux

### 静态路由

### 处理更新阻塞


## API
### MemoryRouter 记忆路由















