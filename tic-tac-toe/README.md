This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

在 React 组件的构造方法 constructor 当中，你可以通过 this.state 为该组件设置自身的状态数据。我们来试着把棋盘格子变化的数据储存在组件的 state 当中吧

在使用 JavaScript classes 时，你必须调用 super(); 方法才能在继承父类的子类中正确获取到类型的 this 。
我们需要判断哪个玩家获胜，并在 X 或 O 两方之间交替落子

使用了 .slice() 方法来将之前的数组数据浅拷贝到了一个新的数组????

**不可变性好处：**

1. 轻松地实现 撤销/重做以及时间旅行

2. 记录变化

** 函数定义组件：**

组件的 keys 值并不需要在全局都保证唯一，只需要在当前的节点里保证唯一即可。

功能相当丰富的井字棋游戏：

1. 实现了井字棋游戏的基本规则并可以进行游戏，
2. 能够判断一方获胜，
3. 能够存储每一步时的棋局状态，
4. 允许玩家切换至之前的某一步“悔棋”。
