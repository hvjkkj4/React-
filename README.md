# React


## React入门

### 简介

#### 是什么

是一个将数据渲染为 HTML 视图的开源 JavaScript 库

+ 发送请求获取数据
+ 处理数据（过滤 整理格式等）
+ **操作 DOM 呈现页面 (react 做这个)**

#### 谁开发的  

由 Facebook 开发，且开源

#### 为什么要学

- 原生 js 操作 DOM 频繁，效率低（ DOM-API 操作 UI ）
- 原生 js 直接操作 DOM，浏览器会进行大量的重绘重排
- 原生 js 没有组件化编码方案，代码复用率低

```react
<ul class="list"></ul>
<script>
  let myStr = ''
  let personStr = [
    { id: 1, name: '小明', age: 18 },
    { id: 2, name: '小红', age: 19 },
  ]
  personStr.forEach((person) => {
    myStr += `<li>${person.name} ${person.age}</li>`
  })
  document.querySelector('.list').innerHTML = myStr
</script>
```

####  React 的特点

- 采用组件化模式，声明式编码，提高开发效率及组件复用率
- 在 React Native 中可以使用 React 语法进行移动端开发
- 使用虚拟DOM优秀的Diffing算法，尽量减少与真实DOM的交互【最重要】

#### 需要掌握的js知识

- 判断this的指向

- class（类）

- ES6语法规范

- npm包管理器

- 原型 原型链

- 数组常用方法

- 模块化

  ​

### jsx语法

#### Hello react

```javascript
<!-- 创建一个容器 -->
<div class="test"></div>

<!-- 引入react核心库 -->
<script type="text/javascript" src="../js/react.development.js"></script>
<!-- 引入react-dom，用来操作DOM -->
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<!-- 引入Babel，把jsx转换为js -->
<script type="text/javascript" src="../js/babel.min.js"></script>

<script type="text/babel"> /* 此处一定是babel */
  // 创建虚拟DOM
  const VDOM = <h1>hello react</h1>  /* 不用加引号，不是字符串，是虚拟DOM */
  // 渲染页面
  ReactDOM.render(VDOM, document.querySelector('.test'))
</script>
```

#### 虚拟DOM

- 本质是Object类型的对象（一般对象）
- 虚拟DOM属性较少，真实DOM属性较多，因为虚拟DOM是React内部在用，不需要那么多属性
- 虚拟DOM最终会转化成真实DOM，渲染在页面上

~~~html
<ul class="list"></ul>
<script>
  let myStr = ''
  let personStr = [
    { id: 1, name: '小明', age: 18 },
    { id: 2, name: '小红', age: 19 },
  ]
  personStr.forEach((person) => {
    myStr += `<li>${person.name} ${person.age}</li>`
  })
  document.querySelector('.list').innerHTML = myStr
</script>
~~~

#### jsx语法规则

+ 虚拟 DOM 不要用引号，``const VDOM=()``
+ **用 js 表达式要用``{}``**
+ **外联样式**，class要改成``className``，id就是``id``
+ **内联样式**，``style={{color:'red',fontSize:'20px'}}``
+ 只能有一个根标签
+ 标签要闭合
+ 标签首字母
  + 若小写字母开头，则将该标签转为html中同名元素，若找不到，则报错
  + 若大写字母开头，react就去渲染对应的组件，若组件没有定义，则报错

~~~react
<!-- 盒子 -->
<div class="test"></div>

<!-- 引入 -->
<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>

<!-- 虚拟DOM渲染页面 -->
<script type="text/babel">
    const myData = 'hello react'
    const myId = 'xie'

    // 1.创建虚拟DOM
    const VDOM = (
      <div>
        <h1 className="box" id={myId}>
          <span>{myData}</span>
        </h1>
        <h1 className="box" id={myId}>
          <span style={{ color: 'red', fontSize: '20px' }}>{myData}</span>
        </h1>
      </div>
    )

    // 2.渲染到页面
    ReactDOM.render(VDOM, document.querySelector('.test'))
</script>
~~~

#### jsx小练习

{}中包括的是js表达式

区分**【js表达式】**和**【js语句（代码）】**

表达式必然有返回值，如:``a``  `a+b`  ``fun(1)``  `arr.map(()=>{})`   `function test(){}`

语句（代码）：`if(){} `  `for(){}`  `switch(){case}`

```javascript
<script type="text/babel">
  // 要区分【js表达式】和【js语句（代码）】

  let data = ['Angular', 'React', 'Vue']

  const VDOM = (
  <div>
    <h1>前端js框架列表</h1>
    <ul>
      {
        data.map((item, index) => {
          return <li key={index}>{item}</li> /* 每个li要有唯一标识 */
        })
      }
    </ul>
  </div>
  )

  ReactDOM.render(VDOM, document.querySelector('.test'))
</script>
```



## React面向组件编程

### 基本理解与应用

#### 函数式组件

组件名必须大写，必须有返回值

标签必须闭合

经过Babel编译后启用了严格模式，this不指向window，而是undefined

React读到ReactDOM.render(<MyComponent />....后

+ 解析MyComponent标签，发现是组件
+ 组件是函数定义的，运行函数，把虚拟DOM转换成真实DOM，呈现在页面

```javascript
<script type="text/babel">    
  function MyComponent() {
    console.log(this)  //undefined
    return '这是函数式组件（简单组件）'
  }

  // 用函数式组件渲染页面
  ReactDOM.render(<MyComponent />, document.querySelector('.test')) 
</script>
```

#### 类的知识复习

+ 类中对变量进行初始化时，需要加构造器
+ B类继承A类，且A类有构造器，B类的构造器中必须调用super（）
+ 类中定义的方法，都绑定在该类的原型对象上，供实例使用

```html
<script>
  class Person {
    constructor(name, age) {
      this.name = name
      this.age = age
    }
    speak() {
      console.log(this)
      console.log(`我叫${this.name}，今年${this.age}岁了`)
    }
  }

  class Student extends Person {
    constructor(name, age, grade) {
      super(name, age)
      this.grade = grade
    }
    speak() {
      console.log(this)
      console.log(`我叫${this.name}，今年${this.age}岁了,在读${this.grade}`)
    }
    study() {
      console.log('每天都在努力学习')
    }
  }

  // const p1 = new Person('小敏', 18)
  // const p2 = new Person('小黑', 20)
  // p1.speak()
  // p2.speak()
  const s1 = new Student('小白', 15, '高一')
  s1.speak()
  s1.study()
</script>
```

#### 类式组件

+ 类式组件必须继承``React.Component``
+ 必须有``render（）``方法
+ 必须有返回值
+ render是放在哪里的？
  + 挂载到MyComponent的原型对象上，供实例对象使用
+ render中的this指什么？
  + MyComponent 组件实例对象（MyComponent 实例对象）
+ 读到``ReactDOM.render(<MyComponent />...``后
  + 1.解析MyComponent标签，发现是组件
  + 2.组件是由类定义的，调用render（），react自己new出一个实例，``实例.render()``
  + 3.将虚拟DOM转换成真实DOM，渲染在页面上

```javascript
<script type="text/babel">
  class MyComponent extends React.Component {
    render() {
      console.log(this)
      return '这是类式组件（复杂组件）'
    }
  }
  ReactDOM.render(<MyComponent />, document.querySelector('.test'))
</script>
```



### 组件三大属性：1.state

#### state初始化

```javascript
class Weather extends React.Component {
  constructor(props) {
    super(props)
    // 初始化state
    this.state = { isHot: false }
  }

  render() {
    console.log(this)
    // 读取state
    return <h1>今日天气{this.state.isHot ? '炎热' : '凉爽'}</h1>
  }
}

ReactDOM.render(<Weather />, document.querySelector('.test'))
```

#### 点击事件复习

```html
<button class="btn1">按钮1</button>
<button class="btn2">按钮2</button>
<button onclick="demo()">按钮3</button>

<script>
  const btn1 = document.querySelector('.btn1')
  btn1.addEventListener('click', () => {
    alert('按钮1被点击了了')
  })

  const btn2 = document.querySelector('.btn2')
  btn2.onclick = () => {
    alert('按钮2被点击了了')
  }

  // react用这种形式
  function demo() {
    alert('按钮3被点击了了')
  }
</script>
```

#### react绑定点击事件

react中，onclick要改为`onClick`，”demo（）“要改为`{demo}`

```javascript
class Weather extends React.Component {
  constructor(props) {
    super(props)
    // 初始化state
    this.state = { isHot: false }
  }

  render() {
    console.log(this)
    // 读取state
    return <h1 onClick={demo}>今日天气{this.state.isHot ? '炎热' : '凉爽'}</h1>
  }
}

function demo() {
  console.log('标题被点击')
}
```

#### this指向问题

+ changeWeather放在哪里？——Weather的5原型对象上，供实例使用
+ 由于changeWeather是作为onClick的回调，所以不是通过实例调用的，是直接调用
+ 类中的方法默认开启了局部的严格模式，所以changeWeather中的this为undefined
+ `w.weatherChange()`   **通过实例调用**，this指向
  + Weather（类名）
+ `this.weatherChange `   **直接调用**，this指向
  + window
  + undefined（类中或严格模式）

```javascript
class Weather extends React.Component {
  constructor(props) {
    super(props)
    this.state = { isHot: true }
  }

  render() {
    return <h1 onClick={this.weatherChange}>今日天气{this.state.isHot ? '炎热' : '凉爽'}</h1>
  }

  weatherChange() {
    console.log(this)  //undefined
    console.log('点击')
  }
}
```

#### 解决this指向问题

`        this.weatherChange = this.weatherChange.bind(this)`

- bind（）可以让this指向变为括号中的内容


- `this.weatherChange.bind(this)`  顺着原型链找到原型对象weatherChange，给weatherChange函数的this指向改为 Weather原型的实例
- `this.weatherChange`  这个新函数挂载在weatherChange属性上

```javascript
class Weather extends React.Component {
  constructor(props) {
    super(props)
    this.state = { isHot: true }
    // 解决this指向问题
    this.weatherChange = this.weatherChange.bind(this)
  }

  render() {
    return <h1 onClick={this.weatherChange}>今日天气{this.state.isHot ? '炎热' : '凉爽'}</h1>
  }

  weatherChange() {
    console.log(this) //Weather
    console.log('点击')
  }
}
```

或者便于更深入的理解，可以改成下方代码

+ bind（）可以让this指向变为括号中的内容


+ `this.demo.bind(this)`  顺着原型链找到原型对象demo，给demo函数的this指向改为 Weather原型的实例
+ `this.test`  这个新函数挂载在test属性上

```javascript
class Weather extends React.Component {
  constructor(props) {
    super(props)
    this.state = { isHot: true }
    // 解决this指向问题
    this.test = this.demo.bind(this)
  }

  render() {
    return <h1 onClick={this.test}>今日天气{this.state.isHot ? '炎热' : '凉爽'}</h1>
  }

  demo() {
    console.log(this) //Weather
    console.log('点击')
  }
}
```

#### setState

+ state更新是合并，不是替换
+ constructor调用了几次？——1次
+ render调用了几次？——1+n次，n为更新状态的次数
+ constructor调用了几次？——n次，n为点击的次数

```javascript
class Weather extends React.Component {
  constructor(props) {
    super(props)
    // 初始化状态
    this.state = { isHot: true }
    // 解决this指向问题
    this.weatherChange = this.weatherChange.bind(this)
  }

  render() {
    return <h1 onClick={this.weatherChange}>今日天气{this.state.isHot ? '炎热' : '凉爽'}</h1>
  }

  weatherChange() {
    console.log(this) //Weather
    this.setState({ isHot: !this.state.isHot })
  }
}
```

#### state简写

+ 箭头函数没有this，会继承外层作用域的this（组件实例），weatherChange为实例对象
+ 普通函数this为undefined，通过bind让this指向组件实例，weatherChange为原型对象（可以在原型链上找到）

```javascript
class Weather extends React.Component {
  // 初始化状态
  state = { isHot: true }

  render() {
    return <h1 onClick={this.weatherChange}>今日天气{this.state.isHot ? '炎热' : '凉爽'}</h1>
  }

  // 自定义方法，使用语句赋值形式加箭头函数
  weatherChange = () => {
    this.setState({ isHot: !this.state.isHot })
  }
}
ReactDOM.render(<Weather />, document.querySelector('.test'))
```



###  组件三大属性：2.props

#### props基本使用

```javascript
class Person extends React.Component {
  render() {
    const { name, gender, age } = this.props
    return (
      <ul>
        <li>姓名：{name}</li>
        <li>性别：{gender}</li>
        <li>年龄：{age}</li>
      </ul>
    )
  }
}

ReactDOM.render(<Person name="Tom" gender="男" age="18" />, document.querySelector('.test1'))
ReactDOM.render(<Person name="David" gender="男" age="20" />, document.querySelector('.test2'))
ReactDOM.render(<Person name="Jenny" gender="女" age="19" />, document.querySelector('.test3'))
```

#### 批量传递props

+ props（多种属性）
+ 展开运算符能不能展开对象？
  + 不能
  + 在react+babel中，传递标签属性
+ `{...p}`是什么含义？
  + 在原生js中，用来复制对象，`let data2 = { ...data }`
  + 在react中，就是`...p`，花括号起到分隔符的作用

```javascript
const p = { name: 'Jenny', gender: '女', age: 19 }
// console.log(...p)  // 无意义，不能随便用
ReactDOM.render(<Person {...p} />, document.querySelector('.test3'))
```

#### 展开运算符复习

以下是展开运算符的几个作用

```javascript
let arr1 = [1, 3, 5, 7]
let arr2 = [2, 4, 6, 8]
// 展开数组
console.log(...arr1)
// 拼接数组
let arr3 = [...arr1, ...arr2]
console.log(arr3)

// 函数应用
function sum(...numbers) {
  return numbers.reduce((preValue, currentValue) => {
    return preValue + currentValue
  })
}
console.log(sum(3, 4))

// 复制对象
let data = { name: 'Tom', age: 30 }
// console.log(...data)  //报错，不能展开对象
console.log({ ...data })

// 复制对象并修改属性
let data2 = { ...data }
data2.name = 'Jerry'
console.log(data)
console.log(data2)
```

#### 限制props

```javascript
// 限制标签属性的类型和必要性
Person.propTypes = {
  name: PropTypes.string.isRequired,
  gender: PropTypes.string,
  age: PropTypes.number,
  speak: PropTypes.func,
}

// 设置标签属性默认值
Person.defaultProps = {
  gender: '男',
  age: 25
}
```

#### props简写方式

+ static关键字，从类的实例转变成类本身的属性
+ 类中constuctor构造器几乎不写
+ 构造器是否接收props，是否传给super，取决于：是否需要通过实例访问props（几乎不会）

```javascript
<!-- 三个盒子 -->
<div class="test1"></div>
<div class="test2"></div>
<div class="test3"></div>

<!-- react底层逻辑 -->
<script type="text/javascript" src="../js/react.development.js"></script>
<!-- 支持react控制DOM -->
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<!-- 把jsx转换为js -->
<script type="text/javascript" src="../js/babel.min.js"></script>
<!-- 对props进行限制 -->
<script type="text/javascript" src="../js/prop-types.js"></script>

<script type="text/babel">
  // 创建类式组件
  class Person extends React.Component {
    // 限制标签属性的类型和必要性
    static propTypes = {
      name: PropTypes.string.isRequired,
      gender: PropTypes.string,
      age: PropTypes.number,
      speak: PropTypes.func,
    }

    // 设置标签属性默认值
    static defaultProps = {
      gender: '男',
      age: 25
    }

    render() {
      const { name, gender, age } = this.props
      return (
        <ul>
          <li>姓名：{name}</li>
          <li>性别：{gender}</li>
          <li>年龄：{age + 1}</li>
        </ul>
      )
    }
  }

  function speak() {
    console.log('说话')
  }
  // 渲染到页面
  ReactDOM.render(<Person name="Tom" gender="男" age={18} speak={speak} />, document.querySelector('.test1'))
  ReactDOM.render(<Person name="Jack" gender="男" age={19} />, document.querySelector('.test2'))
  const p = { name: 'Jenny', gender: '女', age: 20 }
  ReactDOM.render(<Person {...p} />, document.querySelector('.test3'))
</script>
```



### 组件三大属性：3.refs

#### ❌字符串形式的ref（过时）

```javascript
class Demo extends React.Component {
  // 点击按钮显示左边文字
  showData1 = () => {
    const { input1 } = this.refs
    alert(input1.value)
  }

  // 失去焦点显示右边文字
  showData2 = () => {
    const { input2 } = this.refs
    alert(input2.value)
  }

  render() {
    return (
      <div>
        <input ref="input1" type="text" placeholder="请输入文字" />&nbsp;
        <button onClick={this.showData1}>点击按钮显示文字</button>&nbsp;
        <input ref="input2" onBlur={this.showData2} type="text" placeholder="失去焦点显示文字" />&nbsp;
      </div>
    )
  }
}
ReactDOM.render(<Demo />, document.querySelector('.test'))
```

#### 回调函数形式的ref

```javascript
class Demo extends React.Component {
  // 点击按钮显示左边文字
  showData1 = () => {
    const { input1 } = this
    alert(input1.value)
  }

  // 失去焦点显示右边文字
  showData2 = () => {
    const { input2 } = this
    alert(input2.value)
  }

  render() {
    return (
      <div>
        <input ref={c => this.input1 = c} type="text" placeholder="请输入文字" />&nbsp;
        <button onClick={this.showData1}>点击按钮显示文字</button>&nbsp;
        <input ref={c => this.input2 = c} onBlur={this.showData2} type="text" placeholder="失去焦点显示文字" />&nbsp;
      </div>
    )
  }
}
ReactDOM.render(<Demo />, document.querySelector('.test'))
```

#### createRef

`React.createRef`调用后可以返回一个容器，该容器可以存储被ref标识的节点，该容器是“专人专用”

```javascript
class Demo extends React.Component {
  // 创造容器
  myRef = React.createRef()
  myRef2 = React.createRef()

  // 点击按钮显示左边文字
  showData1 = () => {
    alert(this.myRef.current.value)
  }

  // 失去焦点显示右边文字
  showData2 = () => {
    alert(this.myRef2.current.value)
  }

  render() {
    return (
      <div>
        <input ref={this.myRef} type="text" placeholder="请输入文字" />&nbsp;
        <button onClick={this.showData1}>点击按钮显示文字</button>&nbsp;
        <input ref={this.myRef2} onBlur={this.showData2} type="text" placeholder="失去焦点显示文字" />&nbsp;
      </div>
    )
  }
}
ReactDOM.render(<Demo />, document.querySelector('.test'))
```



### 事件处理

+ 发生事件的元素也是你要操作的元素时(如第二个输入框焦点事件)，可以不用ref，使用事件处理
+ 通过`onXxx`属性指定事件处理函数（注意大小写）
  + React使用的是自定义（合成）事件，而不是使用原生的DOM事件 ——为了更好的兼容性
  + React中的事件是通过事件委托方式处理的（委托给组件最外层的元素）——为了高效
+ 通过`event.target`得到发生事件的DOM元素对象 ——不要过度使用ref

```javascript
// 失去焦点显示右边文字
showData2 = (event) => {
  alert(event.target.value)
}

render() {
  return (
    <div>
      <input ref={this.myRef} type="text" placeholder="请输入文字" />&nbsp;
      <button onClick={this.showData1}>点击按钮显示文字</button>&nbsp;
      <input onBlur={this.showData2} type="text" placeholder="失去焦点显示文字" />&nbsp;
    </div>
  )
}
```



### 收集表单数据

#### 非受控组件

```javascript
class Login extends React.Component {
  handleSubmit = (event) => {
    event.preventDefault() // 阻止表单提交
    const { username, password } = this
    alert(`你的用户名是${username.value}，你的密码是${password.value}`)
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        用户名：<input ref={c => this.username = c} type="text" name="username" />
        密码：<input ref={c => this.password = c} type="password" name="password" />
        <button>登录</button>
      </form>
    )
  }
}
```

#### 受控组件

```javascript
<script type="text/babel">
  class Login extends React.Component {
    // 初始化状态
    state = {
      username: '',  // 用户名
      password: ''   // 密码
    }

    // 保存用户名到state中
    saveUsername = (event) => {
      this.setState({ username: event.target.value })
    }

    // 保存密码到state中
    savePassword = (event) => {
      this.setState({ password: event.target.value })
    }

    // 表单提交的回调
    handleSubmit = (event) => {
      event.preventDefault() //阻止提交表单
      const { username, password } = this.state
      alert(`你的用户名是${username}，密码是${password}`)
    }

    render() {
      return (
        <form onSubmit={this.handleSubmit}>
          用户名：<input onChange={this.saveUsername} type="text" name="username" />
          密码：<input onChange={this.savePassword} type="password" name="password" />
          <button>登录</button>
        </form>
      )
    }
  }

  ReactDOM.render(<Login />, document.querySelector('.test'))
</script>
```



### 生命周期

#### 引出生命周期

+ 渲染组件：`ReactDOM.render(<类名/>, ...)`
+ 卸载组件：`ReactDOM.unmountComponentAtNode(...)`
+ 组件的亲儿子（生命周期函数，生命周期钩子）
  + 组件挂载到页面：`componentDidMount() {}`
  + 组件将要被卸载：`componentWillunMount(){}`
+ 组件的干儿子(语句赋值形式＋箭头函数)
  + 自定义回调函数：`death = () => {}`

```react
<script type="text/babel">
  class Life extends React.Component {
    // 初始化状态
    state = { opacity: 1 }

    // 自定义回调函数
    death = () => {
      // 卸载组件
      ReactDOM.unmountComponentAtNode(document.querySelector('.test'))
      // 关闭定时器
      clearInterval(this.timer)
    }

    // 组件挂载到页面
    componentDidMount() {
      // 组件一挂载就开启定时器
      this.timer = setInterval(() => {
        let { opacity } = this.state
        opacity -= 0.1
        if (opacity <= 0) opacity = 1
        this.setState({ opacity })
      }, 200)
    }

    // 组件初始化或状态更新
    render() {
      return (
        <div>
          <h2 style={{ opacity: this.state.opacity }}>学不会react怎么办？</h2>
          <button onClick={this.death}>不活了</button>
        </div>
      )
    }
  }

  ReactDOM.render(<Life />, document.querySelector('.test'))
</script>
```

#### 生命周期（旧）

+ 初始化阶段：由ReactDOM.render(）触发，初次渲染
  + constructor()
  + componentWillMount()
  + render()
  + **componentDidMount()**（初始化，如：开启定时器、发送网络请求、订阅消息）
+ 更新阶段：有组件内部this.setState()或父组件重新render触发
  + shouldComponentUpdata()
  + componentWillUpdate()
  + render()
  + componentDidUpdate()
+ 卸载组件：由ReactDOM.unmountComponentAtNode()触发
  + **componentWillUnmount()**（收尾，如：关闭定时器、取消订阅消息）


#### 生命周期（新）

+ 初始化阶段：由ReactDOM.render(）触发，初次渲染
  - constructor()
  - getDerivedStateFromProps
  - render()
  - **componentDidMount()**（初始化，如：开启定时器、发送网络请求、订阅消息）
+ 更新阶段：有组件内部this.setState()或父组件重新render触发
  + getDerivedStateFromProps
  + shouldComponentUpdata()
  + render()
  + getSnapshotBeforeUpdate
  + componentDidUpdate()
+ 卸载组件：由ReactDOM.unmountComponentAtNode()触发
  - **componentWillUnmount()**（收尾，如：关闭定时器、取消订阅消息）


+ react新旧生命周期有什么区别？
  + 废弃了三个，componentWillMount, componentWillUpdate, componentWillReceiveProps（被滥用，有bug，实现异步渲染后更加误用，出现bug）
  + 增加了两个，getDerivedStateFromProps, getSnapshotBeforeUpdate(开发很少用)
+ 经常用的
  + render, componentDidMount, componentWillUnmount



## react应用（基于脚手架）

### react脚手架

+ xxx 脚手架：用来帮助程序员快速创建一个基于 xxx 库的模板项目
  + 包含了所有需要的配置（语法检查、jsx编译、devSever...）
  + 下载了所有相关的依赖
  + 可以直接运行一个简单的效果
+ react提供了一个用于创建reac他、项目的脚手架库：create-react-app
+ 项目的整体技术架构为：react+webpack+es6+eslint
+ 使用脚手架开发的项目特点：模块化，组件化，工程化

### 创建项目并启动

+ 全局安装，npm i create-react-app -g
+ 切换到想创建项目的文件夹，create-react-app hello-react
+ 进入项目文件夹
+ 启动项目：npm start/yarn start(推荐，yarn和react都是facebook开发的)

### react脚手架项目结构

public ---- 静态资源文件夹
		favicon.icon ------ 网站页签图标
		**index.html -------- 主页面**
		logo192.png ------- logo 图
		logo512.png ------- logo 图
		manifest.json ----- 应用加壳的配置文件
		robots.txt -------- 爬虫协议文件

src ---- 源码文件夹
		App.css -------- App 组件的样式
		**App.js --------- App 组件**
		App.test.js ---- 用于给 App 做测试
		index.css ------ 样式
		**index.js ------- 入口文件**
		logo.svg ------- logo 图
		reportWebVitals.js --- 页面性能分析文件(需要 web-vitals 库的支持)
		setupTests.js ---- 组件单元测试的文件(需要 jest-dom 库的支持)

