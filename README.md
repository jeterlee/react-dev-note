# ReactDevNote

![reactjslogo](https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1887081804,2705256642&fm=27&gp=0.jpg)

[TOC]

## 1. React简介{#index}

- **ReactJS官方地址**：[https://facebook.github.io/react/](https://facebook.github.io/react/)
- **GitHub地址**：[https://github.com/facebook/reac](https://github.com/facebook/react)

## 2. React特点

- **虚拟DOM**: React也是以数据驱动的，每次数据变化React都会扫码整个虚拟DOM树，自动计算与上次虚拟DOM的差异变化，然后针对需要变化的部分进行实际的浏览器DOM更新。

- **组件化**： React可以从功能角度横向划分，将UI分解成不同组件，各组件都独立封装，整个UI是由一个个小组件构成的一个大组件，每个组件只关系自身的逻辑，彼此独立。

- **单项数据流**：React设计者认为数据双向绑定虽然便捷，但在复杂场景下副作用也是很明显，所以React更倾向于单向的数据流动-从父节点传递到子节点。（使用ReactLink也可以实现双向绑定，但不建议使用）

## 3. React开发环境搭建 

访问 [https://facebook.github.io/react/](https://facebook.github.io/react/)，在页面中单击网页左上角的React版本。点击后下载两个文件。

- **react.js**：实现React核心逻辑，且于具体的渲染引擎无关，从而可以跨平台公用。如果应用要迁移到React Native，这一部分逻辑是不需要改变的。

- **react-dom.js**：包含了具体的DOM渲染更新逻辑，以及服务端渲染的逻辑，这部分就是与浏览器相关的部分了。

## 4. JSX语法 

JSX即Javascript XML，它使用XML标记来创建虚拟DOM和声明组件。JSX是支持表达式的，你只要使用{}括号，就可以使用表达式了。需要注意的是表达式不支持if…else这样的语句，但是支持三元运算符和二元运算符。JSX允许直接在模版插入JavaScript变量。如果这个变量是一个数组，则会展开这个数组的所有成员。

JSX的优点：

- 可以使用熟悉的语法仿照HTML来定义虚拟DOM。
- 程序代码更加直观。
- 于JavaScript之间等价转换，代码更加直观。

## 5. React组件

React组件可以把它看作带有props属性集合和state状态集合并且构造出一个虚拟DOM结构的对象。

### 5.1 state成员

**注意的点** 

- 组件总是需要和用户互动的。React的一大创新，就是将界面组件看成一个状态机，用户界面拥有不同状态并根据状态进行渲染输出，用户界面和数据始终保持一致。开发者的主要工作就是定义state，并根据不同的state渲染对应的用户界面。

- 通知React组件数据发生变化的方法是调用成员函数setState(data,callback)。这个函数会合并data到this.state,并重新渲染组件。渲染完成后，调用可选的callback回调。（大部分情况下不需要调用回调，因为React会负责把界面更新到最新状态）

- getInitialState函数必须有返回值，可以是null,false,一个对象。

- 访问state数据的方法是”this.state.属性名”。

- 变量用{}包裹，不需要再加双引号。

### 5.2 props和render成员

- props实例

props是组件固有属性的集合，其数据由外部传入，一般在整个组件的生命周期中都是只读的。属性的初识值通常由React.createElement函数或者JSX中标签的属性值进行传递，并合并到组件实例对象的this.props中。

[ *注： 通常固定的组件内只读的、应由父组件传递进来的属性适合放在props集合中，如组件的类名、颜色、字体、事件响应回调函数等。*]

- props与state的区别

    - props不能被其所在的组件修改，从父组件传递进来的属性不会在组件内部更改；
    - state只能在所在组件内部更改，或在外部调用setState函数对状态进行间接修改。

- render成员函数

render是一个函数，它对于组件来说，render成员函数是必需的。render函数的主要流程是检测this.props和this.state,再返回一个单一组件实例。

render函数应该是纯粹的，也就是说，在render函数内不应该修改组件state，不读写DOM信息，也不与浏览器交互。如果需要交互，应该在生命周期中进行交互。

### 5.3 生命周期

一个组件完整的生命周期包含实例化阶段、活动阶段、销毁阶段三个阶段。每个阶段又由相应的方法管理。

过程中涉及三个主要的动作术语：

- mounting:表示正在挂接虚拟DOM到真实DOM。
- updating:表示正在被重新渲染。
- unmounting:表示正在将虚拟DOM移除真实DOM。

每个动作术语提供两个函数：

- componentWillMount()
- componentDidMount()
- componentWillUpdate(object nextProps, object nextState)
- componentDidUpdate(object prevProps, object prevState)
- componentWillUnmount()

### 5.4 this.props.children

this.props对象的属性与组件的属性一一对应，但有一个例外，就是this.props.children属性。它表示组件的所有子节点。

需要注意this.props.children的值有三种可能

- 如果当前组件没有子节点，他就是undfined；
- 如果有一个子节点，数据类型是object；
- 如果有多个子节点，数据类型就是array。所以处理this.proprs.children的时候要小心。

### 5.5 props属性验证

React.PropTypes提供各种验证器（validator）来验证传入数据的有效性。当向props传入无效数据时，React会在JavaScript控制台抛出警告。

使用getDefaultProps方法可以用来设置组件属性的默认值。

### 5.6 获取真实DOM节点

React中的DOM也是虚拟DOM（virtual DOM），这点跟我们以前讲的Vue非常类似。只有当它插入文档以后，才会变成真实的DOM。React也是在虚拟DOM发生变化时，进行比对后，只渲染变化的部分，它是React极高性能的主要原因之一。

[ 注意：*由于this.refs.[refName]属性获取的是真实DOM，所以必须得到虚拟DOM插入文档以后，才能使用这个属性，否则会报错。*]

## License

```
 Copyright (c) 2017, The Jeterlee authors 

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
```

