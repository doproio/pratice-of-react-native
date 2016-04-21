# Frozen-React-Native组件规范

> 本规范是基于airbnb的[react代码规范](https://github.com/airbnb/javascript/tree/master/react)和facebook react的[组件规范和生命周期](https://facebook.github.io/react/docs/component-specs-zh-CN.html)以及广发证券前端团队的[ES6代码规范](https://github.com/gf-rd/es6-coding-style)修改而成。

## 内容目录
	
- React/JSX代码规范
  - [文件与组件命名](#文件与组件命名)
  - [组件声明](#组件声明)
  - [对齐](#对齐)
  - [空格](#空格)
  - [括号](#括号)
  - [标签](#标签)
  - [方法声明的顺序](#方法声明的顺序)
-  Frozen组件规范
	-  [目录规范](#目录规范)
  -  [文档注释](#文档注释) 
	-  [render](#render)
	-  [getDefaultProps](#getDefaultProps)
	-  [propTypes](#propTypes)
- ES6代码风格
  - [变量与常量声明](#变量与常量声明)
  - [解构](#解构)
  - [数组](#数组)
  - [函数](#函数)
  - [类](#类)
  - [模块](#模块)

## React Native/JSX代码规范

### 文件与组件命名

  - **扩展名**: 使用`.js`作为js文件的扩展名。如果同一个文件夹下有同名而不同作用的js文件，则通过中缀（小写）进一步区分，例如：`HomeView.component.js`,`HomeView.css.js`,`HomeView.action.js`等。
  - **文件名**: 使用驼峰命名法且首字母大写，如`HomeView.js`。
  - **组件命名**: 与文件名（除中缀外）完全一致。如果组件单独放置在目录中，则目录名也一致。  
  
    ```javascript
    // bad
    import Footer from './Component/Footer/FooterView'

    // good
    import Footer from './Component/Footer/Footer'

    // good
    import Footer from './Footer'
    ```
### 组件声明
  - 使用class与extends关键字。不使用React.createClass方法。需要导出的组件直接在class关键字前使用export default。
    ```javascript
    // bad
    export default React.createClass({
    });

    // good
    export default class HomeView extends React.Component {
    }
    ```

### 对齐
  - 按下面的案例对齐：

    ```javascript
    // bad
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // good
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // 如果一行能摆下props，那就摆在一行
    <Foo bar="bar" />

    // 子组件照常缩进
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Spazz />
    </Foo>
    ```

### 空格
  - 在自闭合的标签中包含一个空格。
    ```javascript
    // bad
    <Foo/>

    // very bad
    <Foo                 />

    // bad
    <Foo
     />

    // good
    <Foo />
    ```

### state/props
  - 对于多个单词组成的pros，使用驼峰命名法。不使用下划线或连接线。
    ```javascript
    // bad
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    // good
    <Foo
      userName="hello"
      phoneNumber={12345678}
    />
    ```
  - 读取state和props时，使用const与解构，必要时可使用let。不使用var。
    ```javascript
    // bad
    var userName = this.props.userName;
    let checked = this.state.checked;

    // good
    const { userName, age, sex } = this.props;
    const { checked } = this.state;
    ```  

### 括号
  - 当JSX标签超过一行时，使用括号包裹。
    ```javascript
    /// bad
    render() {
      return <MyComponent className="long body" foo="bar">
               <MyChild />
             </MyComponent>;
    }

    // good
    render() {
      return (
        <MyComponent className="long body" foo="bar">
          <MyChild />
        </MyComponent>
      );
    }

    // good, when single line
    render() {
      const body = <div>hello</div>;
      return <MyComponent>{body}</MyComponent>;
    }
    ```

### 标签
  - 对于没有子组件的JSX标签，始终自闭合。
    ```javascript
    // bad
    <Foo className="stuff"></Foo>

    // good
    <Foo className="stuff" />
    ```

  - 如果组件有多行属性，则另起一行进行自闭合。
    ```javascript
    // bad
    <Foo
      bar="bar"
      baz="baz" />

    // good
    <Foo
      bar="bar"
      baz="baz"
    />
    ```


### 方法声明的顺序

  - 原则上按如下顺序排列React组件的各个方法（生命周期）：
  
  1. constructor
  1. 静态方法（static methods)
  1. componentWillMount
  1. componentDidMount
  1. componentWillReceiveProps
  1. shouldComponentUpdate
  1. componentWillUpdate
  1. componentDidUpdate
  1. componentWillUnmount
  1. 点击处理或事件处理函数，比如onClickSubmit()、onChangeDescription()
  1. 用在render中的getter方法，比如getSelectReason()、getFooterContent()
  1. 可选的render方法，比如renderNavigation()、renderProfilePicture()
  1. render

  - 按如下方式定义propTypes, defaultProps, contextTypes等  

  ```javascript
  import React, { Component, PropTypes } from 'react';
  
  const propTypes = {
    id: PropTypes.number.isRequired,
    url: PropTypes.string.isRequired,
    text: PropTypes.string,
  };
  
  const defaultProps = {
    text: 'Hello World',
  };
  
  class Link extends Component {
    static methodsAreOk() {
      return true;
    }
  
    render() {
      return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>
    }
  }
  
  Link.propTypes = propTypes;
  Link.defaultProps = defaultProps;
  
  export default Link;
  ```

**[⬆ 回到目录](#内容目录)**

## 组件规范

### 目录规范

```
├── android
├── component
│   ├── fz
│   │   ├── demo
│   │   ├── font
│   │   ├── img
│   │   ├── index.js
│   │   ├── style
│   │   └── view
│   ├── style
│   │   ├── common
│   │   └── home
│   └── view
│       ├── common
│       └── home
├── index.android.js
├── index.ios.js
├── ios
├── package.json
└── svn-ignore.txt
```
组件及都放在component目录下
- style -- 样式文件存放目录
```
module.exports = require('react-native').StyleSheet.create({
  
});
```

- img -- 图片文件存放目录
- font -- 字体文件存放目录
- demo -- 组件demo存放目录，命名为`xxxExample.js`，例如: `ButtonExample.js`
- view -- 组件存放目录，采用首字母大写的驼峰命名规则，例如: `Button.js`。

### 文档注释
使用esdoc生成文档，写基本的注释用于生成文档：
使用`/**` 开头的注释将用于生成文档。  

- 组件介绍和例子
组件介绍必须，最好提供一到两个使用的例子  

```js
/**
 * Avatar Component
 * @example
 * <Avatar src="xxxxx" size={50} />
 */
```

- 组件参数
当组件有参数的时候必须有组件参数类型，默认值，参数介绍。  

```js
/**
 * This is Avatar constructor.
 * @param {string} props.src - Image src
 * @param {number} [props.size=40] - Avatar size
 */
```
- 一个例子

```js
/**
 * Avatar Component
 * @example
 * <Avatar src="xxxxx" size={50} />
 */
export default class Avatar extends Component {
    /**
     * This is Avatar constructor.
     * @param {object} props
     * @param {string} props.src - Image src
     * @param {number} [props.size=40] - Avatar size
     */
    constructor(props) {
        super(props);
    };
}
```

### render

`render()`是**必须**的，当被调用时,它应该检查 this.props 和 this.state 并返回单个子元素.

也可以返回 null 或 false 来指示你不想要任何东西被渲染.

`render() `函数应该是纯净的,意味着它**不改变组件的状态**,它在每次调用时返回相同的结果,并且它不读和写 DOM 或者其他方式与程序互动(例如,使用 setTimeout).如果你需要与程序互动,在 componentDidMount() 里执行你的工作,或者其他生命周期方法里.保持 `render() `纯净使组件渲染更实用并且让组件更易懂。

### getDefaultProps

在类被创建时调用一次并被缓存.在这个mapping里的值会被设置给 this.props.

这个方法在任何实例被创建之前调用，因此不能依赖于 this.props.另外,小心,任何被 getDefaultProps()返回的复杂对象会被跨实例共享,而不是被拷贝。

如果组件有默认参数，则`getDefaultProps`是**必须**的，而且默认参数应该只在这个方法中维护。

eg:
```javascript
static defaultProps = {
		size: 40,
		color: '#fff',
		backgroundColor: '#bdbdbd'
};
```


### propTypes

如果组件有默认参数，则`propTypes`是**必须**的，而且需要对参数进行类型检查。

eg:

```javascript
static propTypes = {
   src: PropTypes.string,
   size: PropTypes.number,
   color: PropTypes.string,
   backgroundColor: PropTypes.string
};
```

**[⬆ 回到目录](#内容目录)**

##ES6 代码风格

### 变量与常量声明

- 1.1 变量

> 尽量使用`let`来代替`var`，`let`定义块级变量，有助于规避var带来的变量命名问题。


- 1.2 常量

> 对于常量应使用`const`进行声明，命名采用驼峰写法

> 对于使用 不可改变的数据应用`const`进行声明

```js
// 不好
let someNum = 123;
const AnotherStr = '不变的字符串';
let arr = ['不', '变', '数', '组'];
var ANOTHER_OBJ = {
  '不变对象': true
};


// 好
const someNum = 123;
const anotherStr = '不变的字符串';
const arr = ['不', '变', '数', '组'];
const anotherObj = {
  '不变对象': true
};

```

#### 解构

- 3.1 解构语句中不使用圆括号

```js
// 不好
[(a)] = [11]; // a未定义
let { a: (b) } = {}; // 解析出错


// 好
let [a, b] = [11, 22];
```

- 3.2 对象解构

> 对象解构 元素与顺序无关

> 对象指定默认值时仅对恒等于undefined ( !== null ) 的情况生效

- 3.2.1 若函数形参为对象时，使用对象解构赋值

```js
// 不好
function someFun(opt) {
  let opt1 = opt.opt1;
  let opt2 = opt.opt2;
  console.log(op1);
}


// 好
function someFun(opt) {
  let { opt1, opt2 } = opt;
  console.log(`$(opt1) 加上 $(opt2)`);
}

function someFun({ opt1, opt2 }) {
  console.log(opt1);
}
```

- 3.2.2 若函数有多个返回值时，使用对象解构，不使用数组解构，避免添加顺序的问题

```js
// 不好
function anotherFun() {
  const one = 1, two = 2, three = 3;
  return [one, two, three];
}
const [one, three, two] = anotherFun(); // 顺序乱了
// one = 1, two = 3, three = 2


// 好
function anotherFun() {
  const one = 1, two = 2, three = 3;
  return { one, two, three };
}
const { one, three, two } = anotherFun(); // 不用管顺序
// one = 1, two = 2, three = 3
```

- 3.2.3 已声明的变量不能用于解构赋值（语法错误）

```js
// 语法错误
let a;
{ a } = { b: 123};
```

- 3.3 数组解构

> 数组元素与顺序相关

- 3.3.1 交换变量的值

```js
let x = 1;
let y = 2;

// 不好
let temp;
temp = x;
x = y;
y = temp;


// 好
[x, y] = [y, x]; // 交换变量
```

- 3.3.2 将数组成员赋值给变量时，使用数组解构

```js
const arr = [1, 2, 3, 4, 5];

// 不好
const one = arr[0];
const two = arr[1];


// 好
const [one, two] = arr;
```

#### 数组

- 4.1 将类数组(array-like)对象与可遍历对象(如`Set`, `Map`)转为真正数组

> 采用`Array.from`进行转换

```js
// 不好
function foo() {
  let args = Array.prototype.slice.call(arguments);
}


// 好
function foo() {
  let args = Array.from(arguments);
}

```
- 4.2 数组去重

> 结合`Set`结构与`Array.from`

> 使用indexOf，HashTable等形式，不够简洁清晰

```js
// 好
function deduplication(arr) {
  return Array.from(new Set(arr));
}
```

- 4.3 数组拷贝

> 采用数组扩展`...`形式

```js
const items = [1, 2, 3];

// 不好
const len = items.length;
let copyTemp = [];
for (let i = 0; i < len; i++) {
  copyTemp[i] = items[i];
}


// 好
let copyTemp = [...items];
```

- 4.4 将一组数值转为数组

> 采用`Array.of`进行转换

```js
// 不好
let arr1 = new Array(2); // [undefined x 2]
let arr2 = new Array(1, 2, 3); // [1, 2, 3]


// 好
let arr1 = Array.of(2);  // [2]
let arr2 = Array.of(1, 2, 3); // [1, 2, 3]
```

#### 函数

- 5.1 当要用函数表达式或匿名函数时，使用箭头函数(Arrow Functions)

> 箭头函数更加简洁，并且绑定了this

```js
// 不好
const foo = function(x) {
  console.log(foo.name); // 返回'' ，函数表达式默认省略name属性
};

[1, 2, 3].map(function(x) {
  return x + 1;
});

var testObj = {
  name: 'testObj',
  init() {
    var _this = this; // 保存定义时的this引用
    document.addEventListener('click', function() {
      return _this.doSth();
    }, false);
  },
  doSth() {
    console.log(this.name);
  }
};

// 好
const foo = (x) => {
  console.log(foo.name); // 返回'foo'
};

[1, 2, 3].map( (x) => {
  return x + 1;
});

var testObj = {
  name: 'testObj',
  init() {
    // 箭头函数自动绑定定义时所在的对象
    document.addEventListener('click', () => this.doSth(), false);
  },
  doSth() {
    console.log(this.name);
  }
};
```

- 5.1.1 箭头函数书写约定

> 函数体只有单行语句时，允许写在同一行并去除花括号

> 当函数只有一个参数时，允许去除参数外层的括号

```js
// 好
const foo = x => x + x; // 注意此处会隐性return x + x

const foo = (x) => {
  return x + x; // 若函数体有花括号语句块时须进行显性的return
}; 

[1, 2, 3].map( x => x * x);

```
- 5.1.2 用箭头函数返回一个对象，应用括号包裹

```js
// 不好
let test = x => { x: x }; // 花括号会变成语句块，不表示对象


// 好
let test = x => ({ x: x }); // 使用括号可正确return {x:x}
```

- 5.2 立即调用函数 IIFE

> 使用箭头函数

```js
// 不好
(function() {
  console.log('哈');
})();


// 好
(() => {
  console.log('哈');
})();

```

- 5.3 函数参数指定默认值

> 采用函数默认参数赋值语法

```js
// 不好
function foo(opts) {
  opts = opts || {};// 此处有将0，''等假值转换掉为默认值的副作用
}


// 好
function foo(opts = {}) {
  console.log('更加简洁，安全');
}
```

- 5.4 对象中的函数方法使用缩写形式

> 更加简洁

> 函数方法不要使用箭头函数，避免this指向的混乱

```js
// 不好
const shopObj = {
  des: '对象模块写法',
  foo: function() {
    console.log(this.des);
  }
};

const shopObj = {
  des: '对象模块写法',
  foo: () => {
    console.log(this.des); // 此处会变成undefined.des，因为指向顶层模块的this
  }
};

// 好
const des = '对象模块写法'; // 使用对象属性值简写方式
const shopObj = {
  des,
  foo() {
    console.log(this.des);
  }
};
```

#### 类

- 6.1 类名应使用帕斯卡写法(`PascalCased`)

```js
// 好
class SomeClass {

}
```

- 6.1.1 类名与花括号须保留一个空格间距

> 类中的方法定义时，括号 `)` 也须与花括号 `{` 保留一个空格间距

```js
// 不好
class Foo{
  constructor(){
    // constructor
  }
  sayHi()    {
    // 仅保留一个空格间距
  }
}


// 好
class Foo {
  constructor() {
    // constructor
  }
  sayHi() {
    // 仅保留一个空格间距
  }
}
```

- 6.2 使用真正意思上的类Class写法，不使用`prototype`进行模拟扩展

> Class更加简洁，易维护

```js
// 不好
function Dog(names = []) {
  this._names = [...names];
}
Dog.prototype.bark = function() {
  const currName = this._names[0];
  alert(`one one ${currName}`);
}

// 好
class Dog {
  constructor(names = []) {
    this._names = [...names];
  }
  bark() {
    const currName = this._names[0];
    alert(`one one ${currName}`);
  }
}
```

- 6.3 `this`的注意事项

> 子类使用`super`关键字时，`this`应在调用`super`之后才能使用

> 可在方法中`return this`来实现链式调用写法

```js
class Foo {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
}

// 不好
class SubFoo extends Foo {
  constructor(x, y, z) {
    this.z = z; // 引用错误
    super(x, y);
  }
}


// 好
class SubFoo extends Foo {
  constructor(x, y, z) {
    super(x, y);
    this.z = z; // this 放在 super 后调用
  }
  setHeight(height) {
    this.height = height;
    return this;
  }
}
```

#### 模块

- 7.1 使用`import / export`来做模块加载导出，不使用非标准模块写法

> 跟着标准走的人，运气总不会太差

```js
// 不好
const colors  = require('./colors');
module.exports = color.lightRed;


// 好
import { lightRed } from './colors';
export default lightRed;

```

- 7.2 `import / export` 后面采用花括号`{ }`引入模块的写法时，须在花括号内左右各保留一个空格

```js
// 不好
import {lightRed} from './colors';
import { lightRed} from './colors';

// 好
import { lightRed } from './colors';
```

**[⬆ 回到目录](#内容目录)**

