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

  - cssText ：获取/设置计算后的 css 样式，缺点，会清空所有样式

  ```js
  this.querySelector('.sub').style.cssText = 'display:block'
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

- 开启定时器前，先关闭定时器

  - 定时器操作放在任务队列的尾部，等待同步代码执行完后再执行

  ```js
  for (var i = 0; i < 5; i++) {
    setTimeout(function() {
      console.log(i)
    })
  }
  console.log('a')
  //输出 a 5 5 5 5 5
  // 解决方法
  // 通过闭包实现
  for (var i = 0; i < 5; i++) {
    ;(function(i) {
      //这个匿名函数生成了闭包的效果，新建了一个作用域，这个作用域接收到每次循环的i值保存了下来，即使循环结束，闭包形成的作用域也不会被销毁
      setTimeout(function() {
        console.log(i)
      })
    })(i)
  }

  // let关键字劫持了for循环的块作用域，产生了类似闭包的效果。并且在for循环中使用let来定义循环变量还会有一个特殊效果：每一次循环都会重新声明变量i，随后的每个循环都会使用上一个循环结束时的值来初始化这个变量i。
  for (let i = 0; i < 5; i++) {
    setTimeout(function() {
      console.log(i)
    })
  }
  ```

- slice 浅拷贝，原数组内的拷贝对象修改了，拷贝过去的对象也会修改掉

- 判断字符串中，字符出现的次数

  ```js
  var str = 'kaikebak'
  var str3 = str.split('k')
  console.log(str3.length - 1) // k 出现的次数
  ```

#### 数组排序

- sort（ function( a , b ){} ）
  - 可选参数。默认根据字符串的 unicode 码进行排序

> 如果 a-b 的结果
>
> ​ 大于 0 ：b 排到 a 前面
>
> ​ 小于 0：a 排到 b 前面
>
> ​ 等于 0：a 和 b 的位置不变

#### 随机排序

Math.random() - 返回一个 0 ~ 1 之间的值，包含 0，不包含 1；

```js
var arr = ['a', 'b', 'c', 'd']

arr.sort(function(a, b) {
  // return
  return Math.random() - 0.5
})
console.log(arr)
```

#### 数组新增方法

- Array.from(lis) , [...lis]
  - 将一个类数组转换为真数组

* forEach（callback（ele，index，array）[，thisArg]）
  - **对数组中的每一个元素，执行一次提供的函数，返回 undefined**
  - 参数：
    - callback 执行的函数
      - ele：数组循环中的元素
      - index：元素对应的下标
      - array：当前正在操作的数组
    - thisArg ：决定 callback 中的 this 指向
* filter（callback（ele，index，array）[，thisArg]）
  - **筛选出符合函数中条件的元素，并作为一个新数组返回**
  - 参数
    - callback 条件函数
      - ele：数组循环中的元素
      - index：元素对应下标
      - array：当前正在操作的数组
    - thisAry：决定 callback 中的 this 指向
* map（callback（ele，index，array）[，thisArg]）
  - **由数组中的每一位元素执行函数后的结果，作为新数组的值**
  - 参数：
    - callback 执行的函数
      - ele：数组循环中的元素
      - index：元素对应下标
      - array：当前正在操作的数组
    - thisAry：决定 callback 中的 this 指向
* reduce（callback（result，ele，index，array）[，initiaValue]）
  - **对数组中的每一个元素执行 callback 函数，将结果根据 callback 函数中的条件，返回单个值。**
  - 参数：
    - callback 执行的函数
      - result：上一次累计的结果
      - ele：当前正在操作的元素
      - index：元素对应的下标
      - array：当前正在操作的数组
    - initiaValue：result 的初始值，如果不提供，则将使用数组中的第一个值。
* some（callback（ele，index，array）[，thisArg]）
  - **测试数组中是否至少有一个元素通过了指定函数的测试，结果返回布尔值**
  - 参数：
    - callback 执行的函数
      - ele：数组循环中的元素
      - index：元素对应下标
      - array：当前正在操作的数组
    - thisAry：决定 callback 中的 this 指向
* every（callback（ele，index，array）[，thisArg]）
  - **测试数组中所有的元素是否都通过了指定函数的测试，结果返回布尔值。**
  - 参数：
    - callback 执行的函数
      - ele：数组循环中的元素
      - index：元素对应下标
      - array：当前正在操作的数组
    - thisAry：决定 callback 中的 this 指向

### 对象方法

- Object.keys(obj)
- 返回一个由 key 组成的数组
- Object.values(obj)
- 返回一个由 value 组成的数组

#### 删除对象中的元素

```javascript
delete obj.key
```

#### Math 方法

- 用 Math.min() 和 Math.max() 实现区间

```js
// 最小0，最大10
var btn = document.querySelectorAll('button')
var span = document.querySelector('span')
btn[0].onclick = function() {
  var num = Number(span.innerHTML) - 1
  num = Math.max(0, num) // 返回最大值
  span.innerHTML = num
}
btn[1].onclick = function() {
  var num = Number(span.innerHTML) + 1
  num = Math.min(10, num)
  span.innerHTML = num
}
```

- break 也能结束 for 循环

#### 递归

- 递归

  ```js
  // var arr = ['html', 'css', ['js']];
  // 数组扁平化
  // var newArr = [];
  // for (var i = 0; i < arr.length; i++) {
  //     if (Array.isArray(arr[i])) {
  //         for (var j = 0; j < arr[i].length; j++) {
  //             if (Array.isArray(arr[i][j])) {

  //             } else {
  //                 newArr.push(arr[i][j])
  //             }
  //         }
  //     } else {
  //         newArr.push(arr[i])
  //     }
  // }
  // console.log(newArr);
  // 封装
  // loop(arr);
  // function loop(parma) {
  //     for (var i = 0; i < parma.length; i++) {
  //         if (Array.isArray(parma[i])) {
  //             loop(parma[i])
  //         } else {
  //             newArr.push(parma[i])
  //         }
  //     }
  // }

  // console.log(newArr);
  // 递归 执行顺序
  // var num = 0;
  // loop(num);
  // function loop(num) {
  //     if (num < 5) {
  //         loop(num+1)
  //     }
  //     console.log(num);
  // }
  ```

- 冒泡排序

  ```js
  // var arr = [2, 40, 93, 12, 39, 11]
  // var onoff = false;
  // for (var j = 0; j < arr.length; j++) {
  //     onoff = true;
  //     for (var i = 0; i < arr.length - 1 - j; i++) {
  //         if (arr[i] > arr[i + 1]) {
  //             var temp = arr[i];
  //             arr[i] = arr[i + 1]
  //             arr[i + 1] = temp;
  //             onoff = false;
  //             // console.log(1);
  //         }
  //     }
  //     if (onoff) {
  //         break;
  //     }
  //     console.log(arr);

  // }
  ```

- 数组去重

  ```js
  var arr = ['one', 'two', 'two', 'one', 'three']

  // 方法一
  // var newArr = []
  // arr.forEach(function (e, i, arr) {
  //     if (arr.indexOf(e) == i) {
  //         newArr.push(e)
  //     }
  // })
  // console.log(newArr)

  // 方法二
  // var newArr = []
  // newArr = arr.filter(function (e, i, arr) {
  //     return arr.indexOf(e) == i
  // })
  // console.log(newArr);

  // 对象的特性
  // var obj = {};
  // arr.forEach(function (e) {
  //     obj[e] = e
  // })

  // console.log(obj);
  // var newArr = []
  // for (key in obj) {
  //     newArr.push(obj[key])
  // }
  // console.log(newArr)
  ```

- 表达式，是有结果的，if for 这种都不是
  - 变量 函数调用 运算符 都是表达式

## 问题

1. 两个 for 循环中的 i，会重复吗？
2. 通过 new Date() 创建的对象，里面用数字和字符串的命名区别：由于浏览器兼容问题，不要用字符串
3. 字符串方法 slice 和 substring() 区别：slice 可以对数组操作，substring 不行
4. 随机排序数组的实现

   ```js
   arrLis.sort(function(p1, p2) {
     return Math.random() - 0.5
   })
   ```

5. 类数组转为数组后，用 innerHTML 的方法添加到页面中，出现 objectELementnodelist

   ```js
   // 自己实现的方法
   arrLis.forEach(function(e) {
     // ul.appendChild(e)  // appendChild 接受的参数，节点对象，可以直接用，ie下有兼容性问题
     ul.innerHTML += '<li>' + e.innerHTML + '</li>'
   })
   ```

6. 第十阶段的无极限菜单，之后要再做一下 脑子没绕出来
7. react 中 super()的作用
8. vue 中 新增数组或者对象的处理
9. vue 中 template 作用
10. vue 中筛选性别的例子中， input change 和 click 方法，执行顺序问题

```js
        <div>
            <input @change="chooseSex" type="radio" v-model="gender" value="">所有
            <input @change="chooseSex" type="radio" v-model="gender" value="男">男
            <input @click="chooseSex" type="radio" v-model="gender" value="女">女
        </div>


          methods: {
              chooseSex() {
                  console.log(this.gender);  // ? 第一次获取到到是空,需要点击2次才可以实现
                  if (app.gender == '') {
                      this.user = users
                  } else {
                      this.user = users.filter(ele => {
                          return ele.gender == this.gender
                      })
                  }
              }
          }
        // @change 方法的 this.gender 马上变了，click的打印的还是上一次的值
```

  可以看一下 mdn 上，input 的事件更改 checked 就是用的 change
