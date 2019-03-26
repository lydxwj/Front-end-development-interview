# react

## 1.react生命周期

- #### 初始化阶段：

  getDefaultProps:获取实例的默认属性(即使没有生成实例，组件的第一个实例被初始化CreateClass的时候调用，只调用一次,)

  getInitialState:获取每个实例的初始化状态（每个实例自己维护）

  componentWillMount：组件即将被装载、渲染到页面上（render之前最好一次修改状态的机会）

  render:组件在这里生成虚拟的DOM节点（只能访问this.props和this.state；只有一个顶层组件，也就是说render返回值值职能是一个组件；不允许修改状态和DOM输出）

  componentDidMount:组件真正在被装载之后，可以修改DOM

- #### 运行中状态： 

  componentWillReceiveProps:组件将要接收到属性的时候调用（赶在父组件修改真正发生之前,可以修改属性和状态）

  shouldComponentUpdate:组件接受到新属性或者新状态的时候（可以返回false，接收数据后不更新，阻止render调用，后面的函数不会被继续执行了）

  componentWillUpdate:不能修改属性和状态

  render:只能访问this.props和this.state；只有一个顶层组件，也就是说render返回值只能是一个组件；不允许修改状态和DOM输出

  componentDidUpdate:可以修改DOM

- #### 销毁阶段：

  componentWillUnmount:开发者需要来销毁（组件真正删除之前调用，比如计时器和事件监听器）

- ### 17版本中去掉的生命周期钩子函数

  - componentWillMount
  - componentWillRecieveProps
  - componentWIllUpdate

- ### 新增两个

  - static getDerivedStateFromProps
    会在初始化和update时触发，用于替换componentWillReceiveProps，可以用来控制 props 更新 state 的过程；它返回一个对象表示新的 state；如果不需要更新，返回 null 即可
  - getSnapshotBeforeUpdate
    用于替换 componentWillUpdate，该函数会在update后 DOM 更新前被调用，用于读取最新的 DOM 数据，返回值将作为 componentDidUpdate 的第三个参数

#### 详情参考：

https://www.jianshu.com/p/b634018d118e

## 2.React 16.3新特性Context API

- `React.createContext()`，这样就创建了两个组件

  ```
  import {createContext} from 'react';
  const ThemeContext = createContext({
    background: 'yellow',
    color: 'white'
  });
  ```

- 调用`createContext`方法会返回两个对象，一个是`Provider`，一个是`Consumer`。

- `Provider`是一个特殊的组件。它可以用来给子树里的组件提供数据

  ```
  class Application extends React.Component {
    render() {
      <ThemeContext.Provider value={{background: 'black', color: 'white'}}>
        <Header />
        <Main />
        <Footer />
      </ThemeContext.Provider>
    }
  }
  ```

  value可以是动态的（比如，基于this.state）。对`Provider`数据的修改会引起所有的消费者（consumer）重绘。

- 使用Consumer。

  ```
  const Header = () => {
    <ThemeContext.Consumer>
      {(context) => {
        return (
          <p style={{background: context.background, color: context.color}}>
            Welcome!
          </p>
        );
      }}
    </ThemeContext.Consumer>
  }
  ```

  如果在render Consumer的时候没有嵌套在一个Provider里面。那么就会使用createContext方法调用的时候设置的默认值。

- *Consumer*必须可以访问到同一个*Context*组件。如果你要创建一个新的context，用的是同样的入参，那么这个新建的context的数据是不可访问的。因此，可以把*Context*当做一个组件，它可以创建一次，然后可以export，可以import。

### 详情请参考:

http://www.php.cn/js-tutorial-386621.html

## 3.react优缺点

- **React速度很快**

与其它框架相比，React采取了一种特立独行的操作DOM的方式。它并不直接对DOM进行操作。它引入了一个叫做虚拟DOM的概念，安插在JavaScript逻辑和实际的DOM之间。这一概念提高了Web性能。在UI渲染过程中，React通过在虚拟DOM中的微操作来实对现实际DOM的局部更新。

- **跨浏览器兼容**

虚拟DOM帮助我们解决了跨浏览器问题，它为我们提供了标准化的API，甚至在IE8中都是没问题的。

- **模块化**

为你程序编写独立的模块化UI组件，这样当某个或某些组件出现问题是，可以方便地进行隔离。
每个组件都可以进行独立的开发和测试，并且它们可以引入其它组件。这等同于提高了代码的可维护性。

- **单向数据流让事情一目了然**

Flux是一个用于在JavaScript应用中创建单向数据层的架构，它随着React视图库的开发而被Facebook概念化。它只是一个概念，而非特定工具的实现。它可以被其它框架吸纳。例如，Alex Rattray有一个很好的Flux实例，在React中使用了Backbone的集合和模型。

- **纯粹的JavaScript**

现代Web应用程序与传统的Web应用有着不同的工作方式。例如，视图层的更新需要通过用户交互而不需要请求服务器。因此视图和控制器非常依赖彼此。许多框架使用Handlebars或Mustache等模板引擎来处理视图层。但React相信视图和控制器应该相互依存在一起而不是使用第三方模板引擎，而且，最重要的是，它是纯粹的JavaScript程序。

- **同构的JavaScript**

单页面JS应用程序的最大缺陷在于对搜索引擎的索引有很大限制。React对此有了解决方案。React可以在服务器上预渲染应用再发送到客户端。它可以从预渲染的静态内容中恢复一样的记录到动态应用程序中。
因为搜索引擎的爬虫程序依赖的是服务端响应而不是JavaScript的执行，预渲染你的应用有助于搜索引擎优化。

- **React与其它框架/库兼容性好**

比如使用RequireJS来加载和打包，而Browserify和Webpack适用于构建大型应用。它们使得那些艰难的任务不再让人望而生畏。

- **缺点**

React本身只是一个V而已，所以如果是大型项目想要一套完整的框架的话，也许还需要引入Flux和routing相关的东西。

大多数坑没踩出来

## 4.什么情况下使用redux

- 某个组件的状态，需要共享
- 某个状态需要在任何地方都可以拿到
- 一个组件需要改变全局状态
- 一个组件需要改变另一个组件的状态

## 5.使用react/vue或其他框架，编写一个简单的Todolist组件，可以不考虑样式，点击添加按钮后，可以把input内容加入到下方的列表中，列表中事项点击后，可以删除。

```
import React, { Component } from 'react';
let id = 0;
export default class Todo extends Component {
  constructor(props) {
    super(props)
    this.state = {
      list: [],
      value: '',
    },
    this.$input = React.createRef();
  }
  delete(id) {
    const list = this.state.list.filter(item => {
      return item.id !== id;
    });
    this.setState({
      list,
    });
  }
  add() {
    const value = this.state.value;
    if (value.trim()) {
      const list = this.state.list;
      list.push({
        value,
        id: id++,
      });
      this.setState({
        list,
        value: '',
      });
    }
  }
  change() {
    const value = this.$input.current.value;
    this.setState({
      value,
    });
  }
  __renderList(list) {
    return (
      <ul>
        {list.map(item => {
          return <li key={item.id} onClick={this.delete.bind(this, item.id)}>{item.value}</li>
        })}
      </ul>
    );
  }
  render() {
    const value = this.state.value;
    const list = this.state.list;
    return (
      <div>
        <input value={value} onInput={this.change.bind(this)} ref={this.$input} />
        <button onClick={this.add.bind(this)}>添加</button>
        {this.__renderList(list)}
      </div>
    );
  }
}
```

