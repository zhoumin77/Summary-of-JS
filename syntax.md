# 基础语法

- DOM 操作

  - `style` node.style.color
    css 中的中横杠 到 js 中用驼峰式

    ```js
    background - color
    backgroundColor
    ```

    `判断页面是否有 class元素`

    ```js
    if (document.querySelector('.home'))'
    ```

- 隐式转换
  - `++` 会进行隐式转换，转换为数字型加 1
    `+`在字符串前加一个正号，字符串转为数值型

  - `isNaN` 隐式转换为数值型，number

- 选择，遍历

  - `if` `while` `switch`区别

    >

    switch 是选择语句 结构清晰，判断条件多的情况下用
    if 是判断语句
    while 是循环语句: 不知道要循环次数，或者条件改变循环时一般用

- `for/in`:语句用于循环对象属性。 `foreach`:遍历数组

  ```js
  // for in
  var person = { fname: 'John', lname: 'Doe', age: 25 }
  var text = ''
  var x
  for (x in person) {
    text += person[x]
  }
  // foreach
  var arr = [1, 2, 3]
  arr.foreach(function(v, i, arr) {
    console.log(v)
    console.log(i)
    console.log(arr)
  })
  ```

- `arguments`,特性，length 和下标，例子：参数求和

  ```js
  // 参数求和
  function fn() {
    lg = arguments.length
    var sum = 0
    for (var i = 0; i < lg; i++) {
      sum += arguments[i]
    }
    alert(sum)
  }
  fn(1, 2, 3, 4, 5)
  ```

- `.` 点 和 `[]`中括号都是操作属性的方法，区别
  **中括号可以传递参数**

- 获取非行内式样式方法,三目运算符，只能执行单条语句

  ```js
  function getStyle(obj, attr) {
    var dom = document.querySelector(obj)
    return dom.currentStyle
      ? dom.currentStyle[attr]
      : getComputedStyle(dom)[attr] // 兼容 ie
  }

  console.log(getStyle('.box', 'backgroundColor')) // 获得的是带单位的
  console.log(getStyle('.box', 'width')) // 100px 获得的是带单位的值
  ```

- 必包： 一个函数调用另一个函数的局部变量

  ```js
  function fn() {
    var a = 1
    function fn1() {
      console.log(a)
    }
    fn1()
  }
  fn()

  for (var i = 0; i < li.length; i++) {
    ;(function(i) {
      li[i].onclick = function() {
        alert(i)
      }
    })(i)
  }
  ```

- apply 、 call 、 bind
  执行函数时，改变 this 指向
  区别：
  apply/call ，会立即指向函数
  apply 后跟的参数，第二个参数是一个数组
  call 用逗号分割参数
  bind 不执行函数，返回一个新的函数，执行新的函数，新的函数改变了指向,原来的函数不改变指向

  ```js
  function fn(i) {
    console.log(i)
    console.log(this)
  }
  fn.call(document.body, 1, 2, 4) // 第一个参数，改变this指针到document.body，后面参数是函数的形参
  fn.call(document.body, [1, 2, 3]) // 第一个参数，改变this指针到document.body，第二个参数是函数的形参

  function fn(i) {
    console.log(i)
    console.log(this)
  }
  var newfn = fn.bind(document.body)
  newfn(1)

  // 封装 bind
  function add(a) {
    console.log(a)
    console.log(this)
    // return 1;
  }
  function bind(fn, obj) {
    return function() {
      fn.call(obj, ...arguments)
    }
  }
  var fn2 = bind(add, document.body)
  console.log(fn2)
  fn2(1)
  ```

- 变量提升
   变量提升到最上面，函数在变量下

## 问题

1. 两个 for 循环中的 i，会重复吗？
2. 通过new Date() 创建的对象，里面用数字和字符串的命名区别：由于浏览器兼容问题，不要用字符串