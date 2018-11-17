# 在此处输入标题

标签（空格分隔）： 未分类

---
**react**
```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">

    <title>Hello React!</title>

    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
</head>

<body>

    <div id="root"></div>

    <script type="text/babel">
        // React - React顶级API
        // React DOM - 添加特定于DOM的方法
        // Babel - 一种JavaScript编译器，允许我们在旧浏览器中使用ES6 +
        // 程序的入口点将是root div元素
        class App extends React.Component { //使用ES6类来创建一个名为的React组件App
            render() { //render()方法，这是类组件中唯一需要的方法，用于呈现DOM节点
                return (
                    <h1>Hello world!</h1>//请勿在元素周围使用引号。这被称为JSX
                ); 
            } 
        } 

        ReactDOM.render(<App />, document.getElementById('root'));//使用React DOM render()方法将App我们创建的类呈现到rootHTML中的div中
        //将JavaScript库加载到静态HTML页面并动态渲染React和Babel的方法效率不高，而且难以维护。
    </script>

</body>

</html>
```

**创建React App**
Create React App，这是一个预先配置了构建React应用程序所需的一切的环境。它将创建一个实时开发服务器，使用Webpack自动编译React，JSX和ES6，自动加载CSS文件，并使用ESLint测试和警告代码中的错误。
要进行设置create-react-app，请在终端中运行以下代码
```
npx create-react-app react-tutorial
```
项目目录：
/public和/src目录，与正规一起node_modules，.gitignore，README.md，和package.json。

在/public，我们的重要文件是index.html，它与index.html我们之前制作的静态文件非常相似- 只是一个rootdiv。这次，没有加载任何库或脚本。该/src目录将包含我们所有的React代码.

**JSX，代表JavaScript XML。**
```
const heading = <h1 className="site-heading">Hello, React</h1>;
```
The below code will have the same output as the JSX above
```
const heading = React.createElement(
    'h1',
    {className: 'site-heading'},
    'Hello, React!'
);
```

SX实际上更接近JavaScript，而不是HTML，因此在编写时需要注意几个关键的区别。

 - className用于代替class添加CSS类，而不是classJavaScript中的保留关键字。
 -  JSX中的属性和方法是camelCase - onclick将成为onClick。 
 -  自动关闭标签必须以斜线结尾 - 例如<img />
 -  JavaScript表达式也可以使用花括号嵌入JSX中，包括变量，函数和属性

React中的几乎所有内容都由组件组成，组件可以是类组件或简单组件。
Remove the App class from index.js, so it looks like this.

```
src/index.js

import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(<App />, document.getElementById('root'));
```

```
src/App.js

import React, {Component} from 'react';

class App extends Component {
    render() {
        return (
            <div className="App">
                <h1>Hello, React!</h1>
            </div>
        );
    }
}

export default App;
```

Let’s create another component. We’re going to create a table. Make Table.js, and fill it with the following data.
```
import React, {Component} from 'react';

class Table extends Component {
    render() {
        return (
            <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Job</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Charlie</td>
                        <td>Janitor</td>
                    </tr>
                    <tr>
                        <td>Mac</td>
                        <td>Bouncer</td>
                    </tr>
                    <tr>
                        <td>Dee</td>
                        <td>Aspiring actress</td>
                    </tr>
                    <tr>
                        <td>Dennis</td>
                        <td>Bartender</td>
                    </tr>
                </tbody>
            </table>
        );
    }
}

export default Table;

```

简单组件
```
const TableHeader = () => { 
    return (
        <thead>
            <tr>
                <th>Name</th>
                <th>Job</th>
            </tr>
        </thead>
    );
}
```
```
简单组件
const SimpleComponent = () => { 
    return <div>Example</div>;
}
类组件
class ClassComponent extends Component {
    render() {
        return <div>Example</div>;
    }
}
```

**props使用：**
app.js：
```
import React, {Component} from 'react';
import Table from './Table';
class App extends Component {
    render() {
      const characters = [
        {
            'name': 'Charlie',
            'job': 'Janitor'
        },
        {
            'name': 'Mac',
            'job': 'Bouncer'
        },
        {
            'name': 'Dee',
            'job': 'Aspring actress'
        },
        {
            'name': 'Dennis',
            'job': 'Bartender'
        }
    ];
        return (
          <div className="container">
              <Table  characterData={characters}/>
          </div>
        );
    }
}

export default App;
```
table.js:
```
import React, {Component} from 'react';
const TableHeader = () => { 
    return (
        <thead>
            <tr>
                <th>Name</th>
                <th>Job</th>
            </tr>
        </thead>
    );
}
const TableBody = props => { 
    const rows = props.characterData.map((row, index) => {
        return (
            <tr key={index}>
                <td>{row.name}</td>
                <td>{row.job}</td>
            </tr>
        );
    });

    return <tbody>{rows}</tbody>;
}
class Table extends Component {
    render() {
        const { characterData } = this.props;
        return (
            <table>
                <TableHeader />
                <TableBody characterData={characterData} />
            </table>
        );
    }
}
// 类组件必须包含render()，并且return只能返回一个父元素。
// 注意，如果return包含在一行中，则不需要括号。
export default Table;
```
