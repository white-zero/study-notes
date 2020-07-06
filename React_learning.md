* React
    - 1、视图层框架
        ---> 一个构建用户界面的框架
        ---> 声明式的框架（比如jquery，就是命令式的，指挥哪一个选择器，选择哪一个元素，然后怎么操作他）
                --->只要定义好数据和DOM之间的对应关系就可以了
        ---> 数据驱动DOM，再用事件反馈给数据
    - 2、组件化开发
        ---> 组件组合而不是继承来对代码进行封装（组件组合更加灵活，也不会收到继承里的约束）
        ---> 主要属性： state&&props（state:状态、数据， props:用于父子组件的通信，子组件通过props拿到父组件传来的数据或方法（react组件
间的数据传递方式是由上向下的，需要父组件在props里把操作的方法也传个子组件，通过一种类似回调的方式，让父组件的数据状态发生改变））
    - 3、生命周期
        ---> 一个组件从建立，到存在，最后到销毁的整个过程
    - 4、JSX表达式
        ---> 一种JS扩展的表达式
        ---> 带有逻辑的标记语法，有别于HTML模版（更像是一个脚本，可以随时改变，更加灵活）
        ---> 对样式，逻辑表达式和事件的支持
    - 5、虚拟DOM （是一种埋在框架底层的机制）（优点：1、操作DOM前对数据进行对比，只有数据变化的时候，才去操作DOM 2、会整合DOM操作）
        --->只有在必要的时候才会去操作DOm，通过减少这种低效的操作来增加性能
                ---> 在react中，会把定义好的JSX标记最终转换成一个虚拟的DOM，存在内存里，（因为内存的读取的速度要比操作DOM快得多）
                ---> 如果用户做了对DOM产生变化的操作（虚拟DOM比较操作前后的数据差异）
                ---> 如果有数据差异，统一操作DOM一次，如果比较之后没有差异，就不会操作DOM了
* React总结
    - 简洁：不是指语法，而是当业务内容复杂时，单向数据流和组件化的组合方式会从很大程度上降低问题的复杂度
    - 灵活：在React中可以把一切理解为js，这样在操作的时候会减少很多的束缚，另外，组件提供了多种嵌套方式，数据驱动，生命周期等特点，让开
发变得更顺畅
    - 高效：虚拟DOM的存在，通过减少和优化对DOM的操作，让react在浏览器中有更好的性能表现
    - but
        ---> 思维转换：比如jsx，单向数据流在之前的原生开发中都没有接触过
        ---> 要依赖生态：比如react-router、react-redux等，要学习更多的内容，也更加复杂
        ---> 变动频繁：不向前兼容

<!--more-->


* JSX语法

    - JSX基本语法
```
let jsx = <div> jsx...</div>
ReactDOM.render(
    jsx,
    document.getElementById('app')
)
```
ReactDOM上有一个render的方法，传第一个是react的内容，第二个是选择器（document。getElementById(('app'))
    - ReactDOM


    - 样式处理

1、行内选择器
```
let style = {
    color: 'red',
    fontSize: '20px'
}
let jsx = <div style = {style}> jsx...</div>
ReactDOM.render(
    jsx,
    document.getElementById('app')
)
```

2、className=“xxx” （因为class和类的class重了）

    - 数据逻辑处理

```
let name = 'white-zero'
let names = [A,B,C]
let flag = 'true'
let jsx = (
    <div>
        {/*条件判断*/}
        {
            flag ? <p>I am {name}</p> : <p>I am not {name} </p>
        }
        {/*数组循环*/}
        {
            names.map((name,index) => <p key={index}>I am {name}</p>)
        }
    </div>
)
ReactDOM.render(
    jsx,
    document.getElementById('app')
)
```


* 组件
    - 组件基本结构
      1.函数类型的组件(hooks之后都可以用这种方式吧)
      ```
      function Component(){
          return <div>hello world</div>
      }
      ```
      2.基于类的组件
      ```
      class xxx extends React.Component{
          render(){
              return <div>hello world</div>
          }
      }
      ```
    - state&&props
      1、state && setState
      ```
      class xxx extends React.Component{
          constructor(props){
              super(props)
              this.state = {
                 name = 'white-zero'
              }
          }
          render(){
              setTimeout(()=>{
                  this.setState({
                      name : 'test'
                  })
              })
              return <h1>I am {this.state.name}</h1>
          }
      }
      ```
      2、props
      ```
      class Component extends React.Component{
          constructor(props){
              super(props)
          }
          render(){
              return <h1>I am {this.props.name}</h1>
          }
      }
      ReactDOM.render(
        <div>
            <Component name = "white-zero"/>
        </div>,
        document.getElementById('app')
      )
      ```

    - 事件处理
      1.事件处理方式1
      ```
      class xxx extends React.Component{
          constructor(props){
              super(props)
              this.state = {
                 name = 'white-zero',
                 age = 18
              }
                this.handleClick = this.handleClick.bind(this)
                //绑定this除了用上面的方法，还可以直接在onClick里使用箭头函数
          }
          handleClick(){
                this.setState(
                    age : this.state.age + 1
                )
          }
          render(){
              return (
                <h1>I am {this.state.name}</h1>
                <p>I am {this.state.age} years old</p>
                <button onClick={this.handleClick}>加一岁</button>
                //<button onClick={(e) => {this.handleClick(e)}}>加一岁</button>
              ）
          }
      }
      ```
      2、事件处理方式2
      ```
      class xxx extends React.Component{
          constructor(props){
              super(props)
              this.state = {
                 name = 'white-zero',
                 age = 18
              }
          }
          handleClick(){
                this.setState(
                    age : this.state.age + 1
                )
          }
          onValueChange(){
              this.setState({
                age : e.target.value
              })
          }
          render(){
              return (
                <h1>I am {this.state.name}</h1>
                <p>I am {this.state.age} years old</p>
                <button onClick={(e) => {this.handleClick(e)}}>加一岁</button>
                <input type="text" onChange = {(e) => {this.onValueCHange(e)}}>
              ）
          }
      }
      ```

    - 组件的组合方式
      1、纯组件形式
      ```
      class Component extends React.Component{
          render(){
              return <div>hello world</div>
          }
      }

      class CC extends React.Component{
          render(){
              return <div>
                        <Component/>
                     </div>
          }
      }
      ```
      2、容器组件形式
      方式1:
      ```
      class Title extends React.Component{
          constructor(props){
                super(props)
        }
          render(){
              return <div>
                        {this.props.title}
                     </div>
          }
      }
      ```
      方式2:
      ```
      class Title extends React.Component{
          constructor(props){
                super(props)
        }
          render(){
              return <div>
                        {this.props.children}
                     </div>
          }
      }

      class CC extends React.Component{
          render(){
              return <div>
                        <Title>
                            <span>App span</span>
                        </Title>
                     </div>
          }
      }
      ```

    - 组件间的数据通信
      1、父组件传给子组件(props)
      2、子组件传给父组件(通过在父组件定义改变数据的方法，然后在子组件中用props继承父组件的方法以改变父组件)
      3、兄弟组件间传值（child1传到父组件，再从父组件传到child2，实现child1改变child2的状态）
      ```
      class Father extends React.Component{
          constructor(props){
                super(props)
                this.state = {
                    child2BgColor: '#999',
                    child1BgColor: '#666'
                }
        }
          onChild2BgColorChange(color){
                this.setState({
                    child2BgColor: color
                })
        }
          render(props){
              return (
                    <div>
                        <Child1 child1BgColor={this.state.child1BgColor} changeChild2Color={(color) => {this.onChild2BgColorChange(color)}} />
                        <Child2 bgColor={this.state.child2BgColor}/>
                    </div>
                     )
          }
      }

      class Child1 extends React.Component{
          constructor(props){
                super(props)
          }
          handleClick(){
                this.props.changeChild2Color('red')
          }
          render(){
              return (
                    <div>
                        <h1>child1: {this.props.child1BgColor}<h1>
                        <button onClick = {(e)=>{this.handleClick(e)} }>改变child2的背景颜色</button>
                     </div>
                    )
          }
      }

      class Child2 extends React.Component{
          constructor(props){
              super(props)
          }
          render(){
              return (
                    <div style={{background: this.props.bgColor}}>
                        <h1>Child2背景颜色:{this.props.bgColor</h1>
                     </div>
                     )
          }
      }
      ```

* 生命周期
    - 生命周期的概念：一个组件从建立，到存在，最后到销毁的整个过程
    - 生命周期的作用
        - 生命周期的节点
                --->Mounting：挂载阶段
                --->Updating：运行时阶段（主要处理的是状态更新时引起的变化）
                --->Unmounting：卸载阶段
                --->Error Handling：错误处理(不管逻辑错误)
        - 执行顺序
        - 加载时：
        - 1、constructor
        - 2、componentWillMount(一般用来执行异步函数)
        - 3、render
        - 4、componentDidMount（组件已经挂载成功了）
        - 更新时：
        - 5、(componentWillReceiveProps) 要接收父组件的props时
        - 5、shouldComponentUpdate（return一个true/false，为true后面才继续执行，一般不动，因为render里面虚拟DOM也会自己判断一次，组件前
后有没有更新）
        - 6、componentWillUpdate
        - 7、render
        - 8、componentDidUpdate
        - 9、componentWillUnmount（组件即将销毁，比如做了定时器，在组件消失的时候，要删除以减少内存占用时使用）

* Router和React-Router
    - Router原理
        - 简单说就是允许页面之间相互跳转并记录跳转的关系且能原路返回的机制
        - 路由历史 ： 栈结构，通过入栈和出栈的方式记录页面的访问过程
        - 路由跳转 ： 负责不同页面的跳转动作，并且可以传递参数
        - 事件 ： 用来打开新页面或返回上一个页面，触发的逻辑
    - 常见Router
        - 页面Router(页面重新加载/渲染)
            -> window.location.href = 'http://www.baidu.com'
            -> history.back()
        - Hash Router（只有Hash值在发生变化（跳到某个hash状态上），页面并没有重新加载，实现单页应用使用的最早的一种技术，兼容性不错）
            -> window.location.href = '#test1'
            -> window.onhashchange = function(){
                  console.log('current hash:', window.location.hash)
               }
        - H5 Router（与Hash Router相比，他既能操作Hash，又能操作路径，适用于单页应用）
            -> history.pushState('test','Title','#test1')
            -> history.pushState('test','Title','/user/index')
            -> history.replaceState('test',null.'/index/test')   （替换当前地址）
    - React-Router(官方提供的路由插件，通过调用他的api就能解决路由上的问题，单页应用必备),(直接下载一个react-router-dom即可)
        - 是动态路由，纯react组件
        - 常用组件：
            -> 路由方式, <BrowserRouter>/<HashRouter>
            -> 路由规则, <Route>
            -> 路由选项, <Switch>
            -> 跳转导航, <Link/>/<NavLink>
            -> 自动跳转，<Redirect>

            ```
            class A extends React.Component{
                constructor(props){
                      super(props)
                }
                render(){
                    return(
                        <div>
                            Component A
                        <Switch>     //exact 完全匹配，只有等于/a时，才跳转。
                            <Route exact path={`${this.props.match.path}`}
                                render={(route) => {
                                  return <div>当前组件是不带参数的</div>
                                    }
                                }
                            <Route path={`${this.props.match.path}/:id`}
                                render={(route) => {
                                  return <div> 参数是{route.match.path.id}</div>
                                }}/>
                        </Switch>
                        </div>
                    )
                }
            }

            class B extends React.Component{
                constructor(props){
                      super(props)
                }
                render(){
                    return(
                        <div>
                            Component B
                        </div>
                    )
                }
            }

            class Wrapper extends React.Component{
                constructor(props){
                      super(props)
                }
                render(){
                    return(
                        <div>
                            <Link to="/a">组件A</Link>
                            <Link to="/a/123">带参数的组件A</Link>
                            <Link to="/b">组件B</Link>
                            {this.props.children}
                        </div>
                    )
                }
            }

            ReactDOM.render(
                <Router>
                    <Wrapper>
                        <Route path="/a" component={A}/>
                        <Route path="/b" component={B}/>
                    </Wrapper>
                </Router>
                document.getElementById('app')
            )

            ```

* React数据管理
    - 依靠状态提升来和兄弟元素进行数据交互
        ---> 通过父组件完成（通过找到共同的祖先元素，适用于组件层级扁平，兄弟组件通信情况很少的情况，不适合业务层级很深的情况）
    - 通过发布订阅模式做数据交互
        --->（观察者模式）：有一个订阅中心，组件A发信息给订阅中心，组件B接收 （业务规模小，层级较深的业务）
    - Redux等数据管理工具
        --->组件A发送action给reducer，reducer把state传给store，再由store驱动组件B更改 （适用于业务复杂，组件层级较深，兄弟组件通信密切>的项目）
