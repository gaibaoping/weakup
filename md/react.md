## 1. 什么是react 
> React 是一个用于构建用户界面的JavaScript库
## 2. 安装react 
> $ bower install react babel --save
## 3. 直接在浏览器中使用React![Alt text](./FE4D.tmp.jpg)
> react.js 是 React 的核心库
react-dom.js 是提供与DOM相关的功能,会在window下增加ReactDOM属性
browser.js 的作用是将JSX语法转为JavaScript语法
script中的type属性为text/babel,因为React独有的JSX语法,跟JavaScript不兼容
## 4. ReactDOM.render 
## 5. JSX 语法 
> #### 是一种JS和HTML混合的语法,将组件的结构、数据甚至样式都聚合在一起定义组件,会编译成普通的Javascript。
- 遇到HTML标签(以 < 开头)，就用HTML规则解析
- 遇到代码块(以 { 开头)，就用JavaScript规则解析
- 使用样式时可以让style等于一个样式对象
- 使用样式类时只能使用className=类名,因为class是Javascript关键字
```
var names = ['盖保平','网头衔','沥青'];
var style = {backgroundColor:"blue"};
ReactDOM.render(
    <ul>
        {
            names.map(function (item,index) {
                return <li key={index} className="red" style={style}>{item}</li>
            })
        }
    </ul>,document.getElementById('app')
);
```
## 6. 定义组件
> 我们可以很直观的将一个复杂的页面分割成若干个独立组件,每个组件包含自己的逻辑和样式 再将这些独立组件组合完成一个复杂的页面。 这样既减少了逻辑复杂度，又实现了代码的重用
- 可组合：一个组件可以和其他的组件一起使用或者可以直接嵌套在另一个组件内部
- 可重用：每个组件都是具有独立功能的，它可以被使用在多个场景中
- 可维护：每个小的组件仅仅包含自身的逻辑，更容易被理解和维护
#### 6.1 定义组件 
> React允许将代码封装成组件，然后像插入普通HTML标签一样，在网页中插入这个组件
- 组件类的第一个字母必须大写
- 组件类能且只能包含一个顶层标签
```
var Message = React.createClass({
    //表示此组件渲染的时候长什么样子
    //返回的虚拟DOM结构有且只能有一个顶级标签
    render(){
        return (
            <div>
                hello
            </div>
        );
    }
});
ReactDOM.render(<Message/>,document.getElementById('app'));
```
#### 6.2 组件的属性 
- 每个组件可以有自己的属性,一般用来存放组件初始后不变的数据,比如人的性别，姓名等
- 属性一般用作组件的数据源，一般由父组件传入,比如你的名字一般是由你父母取的
- 属性可以通过this.props中取出
- propTypes可以用来定义传入组件属性的名称和类型
- getDefaultProps函数可以用来定会引起组件的默认属性
```
var Person = React.createClass({
    //类似于约定了一个接口文档,用于这是验证传递给组件的属性，
    propTypes: {
        //定义msg的属性类型为字符串，必须传入
        name: React.PropTypes.string.isRequired,
        gender: React.PropTypes.string.isRequired,
        age:React.PropTypes.number.isRequired
    },
    getDefaultProps:function(){
        return {name:'无名氏'}
    },
    render: function() {
        //属性可以通过属性对象this.props中取出
        return (<h1> {this.props.name}
                     {this.props.gender}
                     {this.props.age}
                </h1>);
    }
});

var props = {
    gender:'男',
    age:18
}

ReactDOM.render(
    <Person {...props} />,//属性可以在使用组件时传入
    document.getElementById('app')
);
```
#### 6.3 state状态 
- 组件的状态就像人的心情，会经常变化，而且只能由自己来改变
- 组件一开始有一个初始状态,然后用户互动,导致状态变化，从而触发界面重新渲染
- getInitialState用来定义初始状态
- 可以给按钮绑定事件，当事件发生的时候调用对应的方法改变组件的状态


----------
