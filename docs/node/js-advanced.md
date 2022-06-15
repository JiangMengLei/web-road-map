# JavaScript高级程序设计(第四版)
## 书籍简介
《JavaScript高级程序设计》是2006年人民邮电出版社出版的图书，作者是(美)(Nicholas C.Zakas)扎卡斯，本书适合有一定编程经验的开发人员阅读，也可作为高校相关专业课程的教材。其在2019年出版了第四版，涵盖ECMAScript 2019，全面、深入地介绍了JavaScript开发者必须掌握的前端开发技术，涉及JavaScript的基础特性和高级特性。书中详尽讨论了JavaScript的各个方面，从JavaScript的起源开始，逐步讲解到新出现的技术，其中重点介绍ECMAScript和DOM标准。在此基础上，接下来的各章揭示了JavaScript的基本概念，包括类、期约、迭代器、代理，等等。另外，书中深入探讨了客户端检测、事件、动画、表单、错误处理及JSON。本书同时也介绍了近几年来涌现的重要新规范，包括Fetch API、模块、工作者线程、服务线程以及大量新API。
## 入手推荐
微信读书65元可购入此书(无限卡可白嫖)，也可以试读前十章，之所以推荐微信读书，是因为电子书上面的代码颜色比较适合阅读，不认识的单词也可以长按查询知道其中文意思和发音，微信读书上还有很多别的书籍，而且大部分是免费的。
## 一、JavaScript和ECMAScript
原文第一章介绍了JavaScript的历史，其实对大多数人来说，并不需要关注JavaScript的历史，但需要知道JavaScript和ECMAScript的关系。  
一句话总结：ECMAScript是一种规范，而JavaScript是实现这种规范的语言。  
对于浏览器来说，除了ECMAScript这种规范，还有W3C(万维网联盟)指定的HTML规范。我们目前常用的浏览器，Chrome、Firefox、Safari、Opera、IE(这个也常用么?)都是根据ECMAScript和W3C指定的规范来实现的，但是规范是规范，实现的方式是不同的，这也就导致了不同的浏览器有不同的实现方式，所以一个让程序员头疼的问题就出现了————浏览器兼容性。  
除了不同浏览器实现的规范方式不同，还有规范本身也在一直更新，比如老的IE8就不支持ECMAScript6，如果你们公司除了需要兼容不同的浏览器的同时，还要兼容浏览器的不同版本，那就真的是男上加男了。  
其实对于现代浏览器来说(上面的除了IE都是)，程序员已经不需要过多关注不同浏览器带来的问题，浏览器本身对于规范的实施比较到位，使用框架也能通过插件完成对不同浏览器的支持，还是需要把精力放在技术本身，这些东西了解下就行。
## 二、在HTML中使用JavaScript
### script标签和script标签属性
可以通过<script></script>标签把JavaScript引入到HTML中，script标签上可以配置几种属性：
- type：指定JavaScript的类型，默认是text/javascript，也可以指定为application/javascript，这样就可以在浏览器中查看到JavaScript代码了。
- async：指定是否异步加载，默认是false，如果是true，那么就是异步加载，如果是false，那么就是同步加载。异步不会阻止浏览器继续加载下面的内容，需保证异步加载的js文件互相之间没有依赖。
- chartset：指定JavaScript的编码，默认是UTF-8，也可以指定为GBK等。
- crossorigin：指定跨域，默认是anonymous，也可以指定为use-credentials。
- defer：指定是否延迟加载，默认是false，如果开启则浏览器会在解析完`</html>`标签后再加载。
- intergrity：指定脚本的完整性，默认是空。
- language：指定JavaScript的语言，默认是JavaScript。(已废弃)
- src：指定JavaScript的路径，默认是空。
  

引入JavaScript的两种方式：
```html
<script src="js/jquery.js"></script>
<!-- 和 -->
<script>
    console.log("hello world");
</script>
```
通过`src`标签引入外部js或直接在`<script>`标签中写入JavaScript代码，这两种方式都可以，前者更容易维护，后者更简单，。
### script的加载顺序
在不适用`async`和`dfer`属性的前提下，会按照html文件标签的顺序加载，如果放进head里就是先加载script再加载页面，为了不阻塞页面，一般放在`body`标签的最后面。  
如果使用`async`，会在加载到script标签时开始加载，但不会阻塞后面的标签加载，加载时间不确定，不完全按照标签顺序加载。  
如果使用`defer`，会按照标签顺序，在加载完`</html>`标签后依序加载。  
### noscript标签
提示用户您的浏览器不支持script。
## 三、基本数据类型
又称为简单数据类型，一共有六种，Symbol是ECMAScript6新增的数据类型。
### Undefined
Undefined数据类型只有一个值就是undefined，声明了一个变量但是没有给他赋值时，该变量的值就是undefined。
```js
let foo;
console.log(foo); // undefined
```
### Null
Null数据类型只有一个值就是null，表示一个空对象指针。
```js
typeof null; // object
```
一般用作初始化一个肯定会赋值的变量。
### Boolean
Boolean数据类型只有两个值，true和false。所有的数据类型都可以通过调用Boolean()函数转换为Boolean数据类型。
```js
null; // false
undefined; // false
0; // false
1; // true
NaN; // false
''; // false
'1'; // true
Object(); // true
```
### Number
#### 浮点数
Number数据类型可以表示数值，包括整数和浮点数。浮点数这里有个0.1+0.2！=0.3的结果，因为浮点数的精度问题。0.1会被换算成二进制进行计算，而0.1的二进制是个无限小数，所以计算出来的结果会是0.300000000000004。一般会采用放大为整数计算再缩小10的倍数。  
浮点数可以用科学计数法表示，如1.23e5，表示1.23×10的5次方，1.23e-5表示1.23×10的-5次方。  
#### 范围
Number不可是无限大的，可以用Infinity表示无限大，-Infinity表示无限小。  
#### NaN
NaN表示Not a Number，即非数字。设计到NaN的所有操作都会返回NaN，可以通过isNaN()函数判断某个变量或表达式是否是NaN。
#### 数值转换
可以用Number()，parseInt()和parseFloat()函数转换为整数和浮点数，具体细节不说了，整数最好用parseInt()，浮点数用parseFloat()。  
### String
字符串类型，可用单引号、双引号、反引号标示。  
几乎所有值都可用toString()转换为字符串。  
### Symbol
就是说Symbol()函数可以给一个不重复的初始值，我把它当成不显示具体值的uuid。  
### 语句
- if语句
- do...while语句
- while语句
- for语句
- for-in语句
- for-of语句
- 标签语句 
- break和continue语句
- with语句(不推荐使用)
- switch语句

## 四、变量、作用域、内存
### 原始值和引用值
原始值就是我们上面提到的六种原始数据类型或称基本数据类型定义的变量的值。原始值和引用值的区别在于：**保存原始值的变量是按值访问的，而保存引用值的变量是按引用访问的，即该值指向的是一个地址**。引用值都是对象，所以通过`typeof`运算符判断变量的类型返回的都是`object`。如果要判断某个引用值变量是通过哪个函数构建的，需要用`instanceof`运算符判断。
原始值变量赋值给别的变量会生成原始值的副本，而引用值变量赋值给其他变量只会复制指针，所以两个变量指向同一个Object。
### 作用域
JavaScript中存在三个作用域：**全局作用域、函数级作用域、块级作用域**。每一个作用域都有一个与其关联的变量对象，这些变量对象之间的关系称为作用域链，它决定了各个作用域执行的顺序，当前作用域可以访问到其上级作用域的方法和变量。<br/>
var是函数作用域，let和const是块级作用域，var声明的变量在整个函数中都可使用，而let和const声明的变量只在其声明的花括号{}内有效。
### 垃圾回收
浏览器回收内存有两种方式，标记清理和引用计数。
#### 标记清理
变量进入执行上下文时会被标记一个声明，变量离开上下文时则打上离开的标记，浏览器会定时回收被打赏离开标记的变量。
#### 引用计数
记录变量被引用的次数，被赋值+1，取消赋值或被覆盖则-1，成0的变量就是可清理变量。不过这种方式有很多问题，例如循环引用，A引用了B，B引用了A，就算AB都离开执行上下文，因为互相引用，也不会被清理，这种方式已经被弃用了。
#### 性能
垃圾回收会影响浏览器性能，所以尽可能减少垃圾回收程序执行的频率。以下列举几个提高性能的点：
- 声明：多用const，少用let，不用var
- 隐藏类：如果两个变量同属一个引用类型(或者说类)，引擎会通过隐藏类将创建的对象关联起来，提高性能，但要注意，如果给其中一个变量声明了不同的属性，则两个变量对应不同的隐藏类。（可能这也是使用TS的一个原因吧）
- 删除属性：不要用delete，变量赋值为null可以不改变隐藏类的关联关系。
- 垃圾回收：降低新建删除对象的频率，可以更改对象的值而不是重新赋值成一个新的对象。
- 内存泄漏：全局变量泄露(声明变量没使用任何关键字)，定时器不用后没有销毁，函数中返回闭包导致函数执行完后没有被销毁，应避免上述操作。
- 静态分配对象池：先创建一个对象池，防止频繁新建销毁对象触发更多的垃圾回收

## 五、基本引用类型
**对象是某个引用类型的`实例`，通过`new`加一个构造函数创建。**
```javascript
let date = new Date()
```
ECMAScript提供了很多原生引用类型供开发者使用：Date，String，Number，Boolean，RegExp。其中，我们把String、Number和Boolean称作原始值包装类型。
直接赋值给变量原始值和通过原始值包装类型给变量赋值不完全相同：
```javascript
let str = 'hello world' // typeof str 'string'
let strObj = new String('hello world') // typeof strObj 'object'
str instanceof String // false
strObj instanceof String // true
```
其他原始值包装类型情况和String类似。
### 一些需要记住的基本引用类型的方法
#### String
- concat:：拼接字符串
- slice、subString：分割字符串，传入起始位置和结束位置
- subStr：分割字符串，传入起始位置和字符个数
- indexOf： 从头查找，返回第一个匹配的位置
- lastIndexOf：从尾查找，返回第一个匹配的位置
- startsWith：是否开始于
- endsWith：是否结束于
- includes：是否包含
- trim、trimLeft、trimRight：去除空格
- repeat：重复
- toLowerCase：转换为小写
- toUpperCase：转换为大写
- replace：替换

#### Number
- toFixed：返回包含指定小数点位数的数值字符串
- toExponential：返回以科学记数法（也称为指数记数法）表示的数值字符串
  
### 单例内置对象
内置对象，或称全局对象(MDN这么称呼的)。要区分内置对象和单例内置对象，Object、Array、String、Date不仅是内置对象，还是引用类型，是可以通过new指令创建实例的。而单例内置对象就真的只是一个对象，可以把他理解为全局唯一的，并且身上挂着很多方法的一个对象，比如说Math，通过console.log输出其实就是这样的：
```javascript
{
    abs:f(),
    cos:f(),
    max:f(),
    min:f(),
    ...
}
```
所以我们这节只需要知道这几个对象，然后明白其中关键几个用法就可以了。
#### Global
globalThis是ES11(ES2020)新加入的全局对象，之前代码并不能够显式的访问到它。我们平时常用的isNaN()、isFinite()、parseInt()和parseFloat()，实际上都是Global对象的方法。
除了这些，还有一些实用的方法：
```javascript
encodeURIComponent：编码
decodeURIComponent：解码
eval：解释器
```
#### Math
Math上有很多非常实用的方法，能够执行复杂的数学计算：
```javascript
min：返回最小值
max：返回最大值
ceil：向上取整
floor：向下取整
round：四舍五入
random：随机数
abs：绝对值
```

## 六、集合引用类型
这章的主要内容是Array、Map、Set。
### Array
数组，一组有序的数据，JS的数组不同于其他语言，数组中每个元素可以不是同类型数据。
#### 创建数组
有下面几种方式：
```javascript
let array = [1,2,3] // 字面量方式创建
let array = new Array(1,2,3) // 通过Array构造函数创建
let array = Array(1,2,3)
```
这上面几种方式得到的结果完全一致。
```javascript
let array = new Array(1,2,3) // [1,2,3]
let array = new Array(123) // 长度为123的数组
```
Array构造函数还有两个ES6新增的用于创建数组的静态方法：from()和of()。from()用于将类数组结构转换为数组实例，而of()用于将一组参数转换为数组实例。
```javascript
let array = Array.from(1,2,3) // [1,2,3]
let array = Array.from('123') // ['1','2','3']
```
#### 数组空位
```javascript
let array = [,] // [null,null]
array[0] // undefined
```
#### 迭代器方法
```javascript
let a = ['red','yellow']
a.keys() // 0,1
a.values() // 'red','yellow'
a.entries() // [0,'red'],[1,'yellow']
```
#### 赋值填充方法
- fill：三个参数，填充值，填充开始索引，填充结束索引
- copyWithin：三个参数，插入位置，复制开始位置，复制结束位置

#### 栈、队列方法
- push：最后插入
- pop：最后弹出
- shift：最前弹出
- unshift：最前插入

#### 排序方法
reverse()可用来反向排列数组，如果想按条件排序，可使用sort()。
sort()默认从小到大排序，也可以接受一个比较函数，比较函数接收两个参数，在函数中判断哪个参数排在前面。
``` javascript
array.sort((a,b)=>{
  return 1 // a排在b后面
  return -1 // a排在b前面
  return 0 // a和b相等
})

```

#### 操作方法
- concat：在数组末尾添加元素
- slice：两个参数，起止位置索引，在本身数组基础上创建一个新数组，不会改变原数组
- splice：三个参数，索引位置，删除元素数量，新插入的元素，返回被删除的元素

#### 搜索和位置方法
- indexOf
- lastIndexOf
- includes
- find 返回元素
- findIndex 返回元素索引
#### 迭代方法
- every 都返回true则返回true
- some 有一个返回true则返回true
- forEach 不返回任何值
- map 返回的值构成一个新数组
- filter 返回的true的元素构成一个新数组

#### 归并方法
reduce()和reduceRight()。

### 定型数组
没搞定

### Map
通过key/value存储的集合。
```javascript
const map = new Map()
map.set('key','value')
map.get('key')
map.size
map.has('key')
map.delete('key')
map.set('key1','value1').set('key2','value2')
map.clear()
```
#### 迭代
可通过for of语句迭代，也可通过keys()、values()、entries()。
#### Object和Map
内存占用：同样内存，Map多存储50%
插入性能：量大的情况，Map更好
查找速度：Object更快
删除性能：Map完胜
#### WeakMap
key只能是Object，key消失则对应值被回收，不可迭代。

### Set
拥有一系列唯一值的集合。
```javascript
const set = new Set()
set.add('value')
set.has('value')
set.size
set.delete('value')
set.add('value1').add('value2')
set.clear()
```
#### 迭代
Set会维护值插入时的顺序，可通过keys()、values()、entries()迭代。

### WeakSet
值只能是Object，值消失则对应值被回收，不可迭代。

## 七、迭代器与生成器
迭代需要在一个有序集合上进行，循环是一种最简单的迭代，但是需要提前知道起始点和长度。
### 迭代器
#### 迭代器模式
我们把实现了Iterable接口的对象称为可迭代对象，他们可通过Iterator(迭代器)消费。
检查一个对象是否可以通过迭代器迭代，可通过下面的方法：
```javascript
let num = 1
console.log(num[Symbol.iterator]) // undefined

let arr = [1,2,3]
console.log(arr[Symbol.iterator]) // function values() { [native code] }
```
迭代器通过`next()`方法遍历数据，next方法返回量个属性，done和value。
每个迭代器都能完成一次完整迭代，互相之间没有联系。
#### 自定义迭代器
通过实现[Symbol.iterator]()方法来创建自定义迭代器。
``` javascript
class Foo {
    [Symbol.iterator]() {
        return {
            next() {
                return { done: true }
            }
        }
    }
}

let foo = new Foo()
console.log(foo[Symbol.iterator]().next()) // {done:true}
```
#### 提前中止迭代器
return()方法，对于for...of，可用break、continue、return或throw提前退出。

### 生成器
生成器拥有在一个函数块内暂停和恢复代码执行的能力。生成器是一个函数，在函数名称前加一个*号表示它是一个生成器。
::: tip 注意
箭头函数不能用来定义生成器函数。
:::
调用生成器函数会生成一个生成器对象，next()方法可以执行生成器。
#### 通过yield中断执行
没有yield的生成器，调用一次next()就会返回{done:true}，函数体中遇到yield，生成器会停止，知道下次调用next()。
yield可以返回值，通过yield返回的值，done为false，通过return返回的值，done为true。
生成器也是一种可迭代对象。
yield还可以当作中间参数使用，通过next()传递的值能通过yield接收。
```javascript
function *foo(t) {
    console.log(t)
    let a = yield t
    console.log(a)
    return t
}

let a = foo(1)
console.log(a.next(2))
console.log(a.next(3))
// 1
// {"value":1,"done":false}
// 3
// {"value":1,"done":true}
```
上面的2没有输出，是因为第一次调用next传入的值是初始化foo是传入的值。
yield * [1,2,3]可以迭代三次。

## 八、对象、类与面向对象编程
对象是一组属性的无序集合。
### 理解对象
对象可通过创建Object的实例创建，或直接通过字面量创建。
#### 数据属性和访问器属性
对象有两种属性：数据属性和访问器属性。
数据属性是保存数据值的位置，有四个特性描述它们的行为：
- [[Configurable]]：是否可以被删除或修改，默认为true。
- [[Enumerable]]：是否可以被for...in循环遍历，默认为true。
- [[Writable]]：是否可以被赋值，默认为true。
- [[Value]]：属性的值，默认为undefined。

访问器属性是一个函数，用来描述对象的属性的读取和设置行为，它包含四个特性：
- [[Configurable]]：是否可以被删除或修改，默认为true。
- [[Enumerable]]：是否可以被for...in循环遍历，默认为true。
- [[Get]]：读取属性的函数。
- [[Set]]：设置属性的函数。
访问器属性不能直接定义，必须通过Object.defineProperty()方法。
如果需要一次定义多个属性，可以使用Object.defineProperties()方法。
```javascript
let persion = {}
Object.definePropertyS(persion, {
    name: {
        value: '张三'
    },
    age: {
        value: 18
    },
    job: {
        get: function() {
            return 'web'
        }
    }
})
```
#### 读取属性特性
使用Object.getOwnPropertyDescriptor()方法可以取得指定属性的属性描述符。返回值是一个对象，对于访问器属性包含configurable、enumerable、get和set属性，对于数据属性包含configurable、enumerable、writable和value属性。ECMAScript 2017新增了Object.getOwnPropertyDescriptors()静态方法，相当于对每个属性调用Object.getOwnPropertyDescriptor()。
#### 合并对象
Object.assign()方法，将源对象的所有可枚举自身属性，复制到目标对象。
#### 相等判定
Object.is()方法，判断两个值是否相等。对于-0，+0，isNaN也能正确返回。
#### 属性简写
属性名和变量名一致时，可以只写变量名。
#### 结构语法
...
### 创建对象

#### Object构造函数或字面量
#### 工厂模式

#### 构造函数模式
通过new+构造函数名，创建一个新对象。
new一个实例的过程如下：
1. 在内存中创建一个新对象。
2. 新对象的__proto__属性指向构造函数的prototype属性。
3. 构造函数内部this指向新对象。
4. 执行构造函数内部代码
5. 构造函数返回新对象。如果手动return，则返回return的内容。
#### 原型模式
每个函数都有一个prototype属性，指向一个对象。
理解原型：
创建一个函数时，会自动获得一个prototype属性，prototype会自动获得一个constructor属性，指向创建函数的构造函数。prototype上的属性是共享的，每一个实例都能访问得到。
判断一个实例对象是否是通过某个构造函数创建的，可以通过以下几种方式：
- instanceof：判断构造函数的prototype属性是否出现在实例对象的原型链上。
- XX.prototype.isPrototypeOf(xx)：判断原型对象是否出现在实例对象的原型链上。
- Object.getPrototypeOf()，返回对象的__proto__属性。

可以通过Object.setPrototypeOf()方法设置一个对象的__proto__属性，但是对性能有很大影响。也可以通过Object.create()创建一个新的对象，同时为其指定原型。

Object.hasOwnProperty()可以判断实例对象上有没有某个属性，in操作符可以判断通过该对象是否能访问到某个属性。这两个结合可以判断实例对象的原型链上是否存在某个属性：xx.hasOwnProperty(name) == false && name in xx == true

for in 可以循环实例对象所有可枚举属性，包括原型对象的属性。Object.keys()只会返回实例对象上的可枚举属性，Object.getOwnPropertyNames()可以返回所有实例属性，包括不可枚举属性。

如果需要重写原型对象，可以在声明构造函数后，直接通过Persion.prototype= {}的方式重写，不过这样会把prototype自带的constructor属性覆盖掉，可以通过defineProperty再定义回来enmuerable设置为false。

#### 对象迭代
Object.values()和Object.entries()接收一个对象，返回它们内容的数组。Object.values()返回对象值的数组，Object.entries()返回键/值对的数组。

### 继承
#### 原型链
每个构造函数都有一个原型对象，原型有个属性指回构造函数，实例对象内部有个指针指向原型对象，如果原型对象也是某个构造函数的实例，那原型对象也有个指针指向它构造函数的原型，这样实例和原型之间就构造了一条原型链。对于绝大多数实例来说，原型链的顶端就是Object.prototype，Object.prototype是一个构造函数，它的原型是null。
#### 盗用构造函数
在子类构造函数中调用父类构造函数，解决原型包含引用值导致的继承问题。
```javascript
function SuperType(name) {
  this.name = name
}
function SubType() {
  // 继承SuperType并传参
  SuperType.call(this, 'Nicholas')
  // 实例属性
  this.age = 29
}
let instance = new SubType()
console.log(instance.name) // "Nicholas";
console.log(instance.age) // 29
```
#### 组合继承
通过原型链继承原型上的方法和属性，通过盗用构造函数继承实例属性。
```javascript
function SuperType(name) {
  this.name = name
  this.colors = ['red', 'blue', 'green']
}
SuperType.prototype.sayName = function () {
  console.log(this.name)
}
function SubType(name, age) {
  // 继承属性
  SuperType.call(this, name)
  this.age = age
}
// 继承方法
SubType.prototype = new SuperType()
```

#### 原型式继承
```javascript
function object(o) {
  function F() {}
  F.prototype = o
  return new F()
}

let person = {
  name: 'Nicholas',
  friends: ['Shelby', 'Court', 'Van']
}
let anotherPerson = object(person)
anotherPerson.name = 'Greg'
anotherPerson.friends.push('Rob')
let yetAnotherPerson = object(person)
yetAnotherPerson.name = 'Linda'
yetAnotherPerson.friends.push('Barbie')
console.log(person.friends) // "Shelby, Court, Van, Rob, Barbie"
```
#### 寄生式继承
创建一个实现继承的函数，以某种方式增强对象，然后返回这个对象。

#### 寄生组合式继承
寄生式组合继承通过盗用构造函数继承属性，但使用混合式原型链继承方法。基本思路是不通过调用父类构造函数给子类原型赋值，而是取得父类原型的一个副本。说到底就是使用寄生式继承来继承父类原型，然后将返回的新对象赋值给子类原型。
```javascript
function object(o) {
  function F() {}
  F.prototype = o
  return new F()
}

function SuperType(name) {
  this.name = name
  this.colors = ['red', 'blue', 'green']
}

SuperType.prototype.sayName = function () {
  console.log(this.name)
}

function SubType(name, age) {
  SuperType.call(this, name) // 盗用继承
  this.age = age
}

function inheritPrototype(subType, superType) {
  let prototype = object(superType.prototype) // 创建对象
  prototype.constructor = subType // 增强对象
  subType.prototype = prototype // 赋值对象
}

inheritPrototype(SubType, SuperType)
```

### 类
```javascript
    // 类声明
    class Person {}
    // 类表达式
    const Animal = class {}
```
类没有提升，受块作用域限制。类可以包含构造函数方法、实例方法、获取函数、设置函数和静态类方法。
```javascript
    // 空类定义，有效
    class Foo {}
    // 有构造函数的类，有效
    class Bar {
      constructor() {}
    }
    // 有获取函数的类，有效
    class Baz {
      get myBaz() {}
    }
    // 有静态方法的类，有效
    class Qux {
      static myQux() {}
    }
```
#### 类构造函数
使用new和类实例化时，会调用类的构造函数，其他操作和实例化构造函数一致。
#### 实例、原型和类成员
在类构造函数中通过this添加的属性会成为实例属性，在类块中定义的方法会成为原型方法。类块中不能添加原始值或对象。类支持设置获取和访问器。
```javascript
class Persion {
    get name() {
        return this._name
    }

    set name(value) {
        this._name = value
    }
}
```
可以在类上定义静态方法，每个类只能定义一个静态方法，在静态方法中，this指向类自身。静态方法将直接加在类身上，而普通方法则加在类的原型上。
静态方法适合作为实例工厂：
```javascript
    class Person {
      constructor(age) {
        this.age_ = age;
      }
      sayAge() {
        console.log(this.age_);
      }
      static create() {
        // 使用随机年龄创建并返回一个Person实例
        return new Person(Math.floor(Math.random()＊100));
      }
    }
    console.log(Person.create()); // Person { age_: ... }
```
类内部不支持添加原型或成员数据，但是外部可以。
```javascript
Person.prototype.name = 'Linda'
Person.name = 'Jack'
```

可以在类内部定义生成器：
```javascript
class Person {
  // 在原型上定义生成器方法
  *createNicknameIterator() {
    yield 'Jack'
    yield 'Jake'
    yield 'J-Dog'
  }
  // 在类上定义生成器方法
  static *createJobIterator() {
    yield 'Butcher'
    yield 'Baker'
    yield 'Candlestick maker'
  }
  // 在原型上定义生成器
  *[Symbol.iterator]() {
    yield* [1, 2, 3]
  }
}
let jobIter = Person.createJobIterator()
console.log(jobIter.next().value) // Butcher
console.log(jobIter.next().value) // Baker
console.log(jobIter.next().value) // Candlestick maker
let p = new Person()
let nicknameIter = p.createNicknameIterator()
console.log(nicknameIter.next().value) // Jack
console.log(nicknameIter.next().value) // Jake
console.log(nicknameIter.next().value) // J-Dog
```
#### 类的继承
通过`extends`可以继承类或者构造函数。
```javascript
class Vehicle {}
// 继承类
class Bus extends Vehicle {}
let b = new Bus()
console.log(b instanceof Bus) // true
console.log(b instanceof Vehicle) // true
function Person() {}
// 继承普通构造函数
class Engineer extends Person {}
let e = new Engineer()
console.log(e instanceof Engineer) // true
console.log(e instanceof Person) // true
```
派生类可通过super调用父类的构造函数。
```javascript
class Vehicle {
  constructor() {
    this.hasEngine = true
  }
  static identify() {
    console.log('vehicle')
  }
}
class Bus extends Vehicle {
  constructor() {
    // 不要在调用super()之前引用this，否则会抛出ReferenceError
    super() // 相当于super.constructor()
    console.log(this instanceof Vehicle) // true
    console.log(this) // Bus { hasEngine: true }
  }
  // 静态方法中可以通过super调用继承父类的静态方法
   static identify() {
    super.identify()
  }
}
new Bus()
Bus.identify() // vehicle
```
::: tip 注意
- super只能在派生类的构造函数和静态方法中使用，要么调用构造函数，要么调用静态方法。
- super()会调用父类的构造方法，并将返回的实例赋值给this。
- 没有定义构造函数会自动调用super()，定义了则必须手动调用super()或返回一个对象。
:::

##### 抽象基类
只能被继承，不能被实例化。
```javascript
// 抽象基类
class Vehicle {
  constructor() {
    console.log(new.target)
    if (new.target === Vehicle) {
      throw new Error('Vehicle cannot be directly instantiated')
    }
  }
}
// 派生类
class Bus extends Vehicle {}
new Bus() // class Bus {}
new Vehicle() // class Vehicle {}
// Error: Vehicle cannot be directly instantiated
```

## 九、代理与反射

### 代理基础
代理是目标对象的抽象，目标对象可通过代理来操作，并施加行为。
```javascript
const target = {
  id: 'target'
}
const handler = {}
const proxy = new Proxy(target, handler)
```
#### 捕获器
可以通过在handler定义一个get方法设置捕获其，捕获其接收目标对象，查询属性，还有代理属性三个参数。
```javascript
    const target = {
      foo: 'bar'
    };
    const handler = {
      get(trapTarget, property, receiver) {
        return trapTarget[property];
      }
    };
    const proxy = new Proxy(target, handler);
    console.log(proxy.foo);   // bar
    console.log(target.foo); // bar
```
可以通过trapTarget[property]重建原始操作。调用全局Reflect方法可以轻松重建原始行为。
```javascript
const target = {
  foo: 'bar'
}
const handler = {
  get() {
    return Reflect.get(...arguments)
  }
}
const proxy = new Proxy(target, handler)
console.log(target.foo) // bar
console.log(proxy.foo) // bar
// 可简写
const handler = {
  get: Reflect.get
}
```
#### 撤销代理
```javascript
    const target = {
      foo: 'bar'
    };
    const handler = {
      get() {
        return 'intercepted';
      }
    };
    const { proxy, revoke } = Proxy.revocable(target, handler);
    console.log(proxy.foo);    // intercepted
    console.log(target.foo);   // bar
    revoke();
    console.log(proxy.foo);    // TypeError
```
#### 反射
- 反射api不限于捕获器
- 大多数反射api在Object有对应方法
#### 代理的代理
#### 代理不能代理Date

### 代理捕获器与反射方法
代理有13种基本操作，这些操作有各自不同的反射API。
1. get(target,property,receiver) => Reflect.get()
可拦截操作：
- proxy.property 
- proxy[property] 
- Object.create(proxy)[property] 
- Reflect.get(proxy,property,receiver)
2. set(target,property,value,receiver) => Reflect.set()
可拦截操作：
- proxy.property=value 
- proxy[property]=value 
- Object.create(proxy)[property]=value 
- Reflect.set(proxy,property,value,receiver)
```javascript
    const myTarget = {};
    const proxy = new Proxy(myTarget, {
      set(target, property, value, receiver) {
        console.log('set()');
        return Reflect.set(...arguments)
      }
    });
    proxy.foo = 'bar';
    // set()
```
返回true表示成功，false表示失败。
3. has(target,property) => Reflect.has()
可拦截操作：
- property in proxy
- property in Object.create(proxy)
- with(proxy) {(property); }
- Reflect.has(proxy, property)
返回true表示存在，false表示不存在。
4. defineProperty(target,property,descriptor) => Reflect.defineProperty()
```javascript
descriptor: {
  enmuerable: true,  // 可枚举
  configurable: true, // 可编辑删除
  writable: true, // 可编辑
  value: 'haha'
}
```
可拦截操作：
- Object.defineProperty(proxy, property, descriptor)
- Reflect.defineProperty(proxy, property, descriptor)

5. getOwnPropertyDescriptor(target,property) => Reflect.getOwnPropertyDescriptor()
6. deleteProperty(target,property) => Reflect.deleteProperty()
可拦截操作：
- delete proxy.property
- delete proxy[property]
- Reflect.deleteProperty(proxy,property)
返回ture表示删除成功，false表示删除失败。
7. ownKeys(target) => Reflect.ownKeys()
可拦截操作：
- Object.getOwnPropertyNames(proxy)
- Object.getOwnPropertySymbols(proxy)
- Object.keys(proxy)
- Reflect.ownKeys(proxy)
8. getPrototypeOf(target) => Reflect.getPrototypeOf()
可拦截操作：
- Object.getPrototypeOf(proxy)
- Reflect.getPrototypeOf(proxy)
- proxy.__proto__
- Object.prototype.isPrototypeOf(proxy)
- proxy instanceof Object
9. setPrototypeOf(target,prototype) => Reflect.setPrototypeOf()
10. isExtensible(target) => Reflect.isExtensible() 是否可拓展的
11. preventExtensions(target) => Reflect.preventExtensions() 方法让一个对象变的不可扩展，也就是永远不能再添加新的属性。
12. apply(target,thisArg,argumentsList) => Reflect.apply() 调用函数时被调用
```javascript
    const myTarget = () => {};
    const proxy = new Proxy(myTarget, {
      apply(target, thisArg, ...argumentsList) {
        console.log('apply()');
        return Reflect.apply(...arguments)
      }
    });
    proxy();
    // apply()
```
可拦截操作：
- proxy(...argumentsList)
- Function.prototype.apply(thisArg, argumentsList)
- Function.prototype.call(thisArg, ...argumentsList)
- Reflect.apply(target, thisArgument, argumentsList)
13. construct(target,argumentsList,newTarget) => Reflect.construct()
```javascript
    const myTarget = function() {};
    const proxy = new Proxy(myTarget, {
      construct(target, argumentsList, newTarget) {
        console.log('construct()');
        return Reflect.construct(...arguments)
      }
    });
    new proxy;
    // construct()
```
可拦截操作：
- new proxy(...argumentsList)
- Reflect.construct(target, argumentsList, newTarget)

### 代理模式
通过捕获get、set、has等操作，监控对象什么时候被修改访问。
隐藏属性（get时返回undefined）
属性验证（set时选择是否设置值）
函数构造参数认证（apply和constructoer时返回失败）

## 十、函数
### 箭头函数
```javascript
let f = (a,b)=> {
  return a+b
}
```
任何可用函数表达式的地方都可以使用箭头函数，声明函数则只能用正式函数。
只有一个参数可以省略括号，只有一行代码可以省略大括号和return。
箭头函数不能使用arguments、super和new.target，也不能用作构造函数。此外，箭头函数也没有prototype属性。

### 参数
函数内部访问arguments对象，会返回每一个参数的值。
### 默认值
```javascript
    function makeKing(name = 'key') {
      return name
    }
```
arguments对象始终以传入的值为准。
### 函数声明与函数表达式
函数声明会有函数声明提升（类似于var的变量提升）。
函数表达式不会提升，用var声明也不会。
### 函数作为值
可以把函数当作变量，当作参数传递给另一个变量。
### 函数内部
arguments
this：引用的是把函数当成方法调用的上下文对象。
谁调用就指向谁，否则指向window
箭头函数中，this指向定义它的上下文。
new.target ： new是指向实例 否则为undefined
### 函数属性与方法
length（命名参数的个数）和prototype（原型对象）
bind()会返回一个新的实例，该实例的this指向bind的参数
### 闭包
闭包指的是那些引用了另一个函数作用域中变量的函数，通常是在嵌套函数中实现的。
闭包的作用域链包含它引用的变量所在函数的作用域。
#### 闭包中的this
每个函数在创建时都会创建两个特殊变量，this和arguments。内部函数永远无法直接访问到外部函数的这两个变量。
内部函数使用箭头函数定义，则this指向定义它的函数的this。
通过函数声明创建函数，则this指向window。
### 立即调用函数表达式
立即调用的匿名函数又被称为立即调用函数表达式(IIFE)。
```javascript
(function(){
 // 块级作用域
})()
```
### 私有变量
函数内部的变量是不能直接在函数外部调用的，但是闭包可以调用。通过返回一个函数达到访问私有变量的目的。
### 静态私有变量
```javascript
(function () {
  let name = ''
  Person = function (value) {
    name = value
  }
  Person.prototype.getName = function () {
    return name
  }
  Person.prototype.setName = function (value) {
    name = value
  }
})()
```
### 单例对象
```javascript
let singleton = (function () {
  // 私有变量和私有函数
  let privateVariable = 10
  function privateFunction() {
    return false
  }
  // 特权/公有方法和属性
  return {
    publicProperty: true,
    publicMethod() {
      privateVariable++
      return privateFunction()
    }
  }
})()
```
## 十一、期约与异步函数
### 异步编程
JS的异步行为会推入一个队列中，当前同步代码执行完毕后，会执行队列中的异步代码。
ES6之前多用回调完成异步操作。
### 期约
```javascript
    let p = new Promise(() => {});
    setTimeout(console.log, 0, p);   // Promise <pending>
```
期约状态：
- 待定（pending）
- 兑现（fulfilled，有时候也称为“解决”, resolved）
- 拒绝（rejected）
期约的执行器函数是同步执行的。
reject会抛出异常，无法通过try...catch捕获。
Promise.resolve()相当于new Promise(resolve=>resolve())。
Promise.reject()相当于new Promise((resolve,reject)=>reject())。
#### Promise的实例方法
- Promise.prototype.then(onResolved, onRejected)
返回一个新的Promise实例，新实例默认通过Promise.resolve()包装返回值，无返回值则为undefined。
- Promise.prototype.catch(onRejected)
事实上，这个方法就是一个语法糖，调用它就相当于调用Promise.prototype.then(null, onRejected)。
catch也会返回一个新的Promise实例。
- Promise.prototype.finally(onFinally)
无论解决还是拒绝，这个方法都会执行，这个方法返回夫期约的传递。
#### 非重入期约方法
即使直接返回fullfilled或rejected的Promise，then中的方法也不会立即执行，而是被推入队列中，等到主线程执行完毕后再执行。

#### 邻近处理程序的执行顺序
先添加到队列的期约先执行，后添加的期约后执行。所以.then().then().then()这种方式实际上是按循序执行的。
#### 期约连锁
.then().then().then()
Promise.all()静态方法创建的期约会在一组期约全部解决之后再解决。
```javascript
    let p = Promise.all([
      Promise.resolve(3),
      Promise.resolve(),
      Promise.resolve(4)
    ]);
    p.then((values) => setTimeout(console.log, 0, values)); // [3, undefined, 4]
```
如果被拒接，则第一个拒绝的理由会传入onRejected方法。
Promise.race()静态方法返回一个包装期约，是一组集合中最先解决或拒绝的期约的镜像。
Promise.race()不会对解决或拒绝的期约区别对待。无论是解决还是拒绝，只要是第一个落定的期约，Promise.race()就会包装其解决值或拒绝理由并返回新期约。
#### 期约扩展
期约取消：resolve之前判断是否执行resolve
进度通知：TODO

### 异步函数
async/await是ES8规范新增的，使得异步代码能够同步执行。
- async关键词用于声明异步函数，可以用在函数声明、函数表达式、箭头函数和方法上。
```javascript
asycn function f() {}
let f = function {}
let f = async () => {}
let o = {
  async f() {}
}
```
异步函数的返回值会用Promise.resolve()包装。在异步函数抛出错误会返回拒绝期约。
- await关键字可以暂停异步函数代码的执行，等待期约解决。
await期待一个Promise实例(不是必须，非异步实例会直接返回)，然后对其解包，返回值是resolve参数的值。
reject需要catch捕获，返回值会被await解包。或者直接使用try...catch捕获。
await只能在异步函数中使用，不能再顶层上下文使用，
调用异步函数在没遇到await之前和同步函数没有区别，遇到await之后，会记录这个位置，等到右边可用了，推送到消息队列中，恢复执行。
```javascript
await async1()
await async2()
await async3()
// 如果三个函数没有前后依赖可以这样改
let a1 = async1()
let a2 = async2()
let a3 = async3()
await a1
await a2
await a3
```
## 十二、BOM
浏览器对象模型（BOM, Browser ObjectModel）。
### window对象
ECMAScript中的Global对象，也是浏览器窗口的JavaScript接口。  
var在全局声明的变量和函数，都会被挂载到window对象上。  
#### 窗口关系
top对象始终指向最上层窗口。  
parent指向当前窗口的父窗口。  
self始终指向window。
#### 窗口位置与像素比
现代浏览器提供了screenLeft和screenTop属性，用于表示窗口相对于屏幕左侧和顶部的位置，返回值的单位是CSS像素。  
可以使用moveTo()和moveBy()方法移动窗口。  
```javascript
    // 把窗口移动到左上角
    window.moveTo(0,0);
    // 把窗口向下移动100 像素
    window.moveBy(0, 100);
    // 把窗口移动到坐标位置(200, 300)
    window.moveTo(200, 300);
    // 把窗口向左移动50 像素
    window.moveBy(-50, 0);
```
**像素比**  
不同设备分辨率不同，高分辨率下的设备应该和低分辨率设备保持1个单位像素大小相同。  
物理像素和实际像素的转换比率由window.devicePixelRatio属性提供。  
#### 窗口大小
innerWidth、innerHeight、outerWidth和outerHeight。outerWidth和outerHeight返回浏览器窗口自身的大小。innerWidth和innerHeight返回浏览器窗口中页面视口的大小（不包含浏览器边框和工具栏）。  
```javascript
    // 缩放到100×100
    window.resizeTo(100, 100);
    // 缩放到200×150
    window.resizeBy(100, 50);
    // 缩放到300×300
    window.resizeTo(300, 300);
```
#### 窗口滚动
```javascript
    // 正常滚动
    window.scrollTo({
      left: 100,
      top: 100,
      behavior: 'auto'
    });
    // 平滑滚动
    window.scrollTo({
      left: 100,
      top: 100,
      behavior: 'smooth'
    });
```
#### 导航与打开新窗口
window.open(url, target, features)  
target可一世一个iframe的id，或者是_blank。。。
#### 定时器
setTimeout()用于指定在一定时间后执行某些代码，而setInterval()用于指定每隔一段时间执行某些代码。  
timeoutID = setTimeout(function,delay,...args)  
为了调度不同代码的执行，JavaScript维护了一个任务队列。其中的任务会按照添加到队列的先后顺序执行。delay只是告诉JS在多少毫秒后把function推到队列中。  
clearTimeout(timeoutID)可以在setTimeout执行前取消执行。  
::: tip 注意
所有超时执行函数的this都指向window，如果需要期调用它的函数的this，可以用箭头函数。
:::
setTimeout和setInterval都是按时往tasks queue中添加任务，当前任务执行完后才会执行下个任务，执行当前代码，回调函数，事件监听回调都会往任务队列添加任务。  
js中不止这一个任务队列，除了Tasks还有Microttasks，当前线的Task运行完成后，会优先处理Microttasks中的任务，Microttasks中的任务处理完后，才会接着处理Tasks中的任务，如果处理Microttasks过程中还有Microttask加进来，会一并处理完成后再处理Tasks。
#### 系统对话框
alert()、confirm()和prompt()方法调用时代码会停止执行，关闭后才会显示
### location对象
window.location和document.location都指向location，location保存着当前加载文档的信息，也保存着把URL解析为离散片段后能够通过属性访问的信息。  
- location.search：返回了url中?开始的内容
URLSearchParams可以解析url参数：
```javascript
    let qs = "? q=javascript&num=10";
    let searchParams = new URLSearchParams(qs);
    alert(searchParams.toString());   // " q=javascript&num=10"
    searchParams.has("num");           // true
    searchParams.get("num");           // 10
    searchParams.set("page", "3");
    alert(searchParams.toString());   // " q=javascript&num=10&page=3"
    searchParams.delete("q");
    alert(searchParams.toString());   // " num=10&page=3"
```
- location.assign(url)
导航到新URL的操作，同时在浏览器历史记录中增加一条记录，相当于：
```javascript
window.location = "http://www.wrox.com";
location.href = "http://www.wrox.com";
```
修改location对象的属性也会修改当前加载的页面：
```javascript
    // 假设当前URL为http://www.wrox.com/WileyCDA/
    // 把URL修改为http://www.wrox.com/WileyCDA/#section1
    location.hash = "#section1";
    // 把URL修改为http://www.wrox.com/WileyCDA/?q=javascript
    location.search = "? q=javascript";
    // 把URL修改为http://www.somewhere.com/WileyCDA/
    location.hostname = "www.somewhere.com";
    // 把URL修改为http://www.somewhere.com/mydir/
    location.pathname = "mydir";
    // 把URL修改为http://www.somewhere.com:8080/WileyCDA/
    location.port = 8080;
```
除了hash之外，只要修改location的一个属性，就会导致页面重新加载新URL，修改hash只会添加一条历史记录。  
- location.replace(url)
这个方法接收一个URL参数，但重新加载后不会增加历史记录。调用replace()之后，用户不能回到前一页。
- location.reload()
它能重新加载当前显示的页面。
```javascript
    location.reload();      // 重新加载，可能是从缓存加载
    location.reload(true); // 重新加载，从服务器加载
```
### navigator对象
navigator对象的属性通常用于确定浏览器的类型。
- navigator.plugins
```javascript
[{
  name:'插件名称',
  description:'插件介绍',
  filename:'插件的文件名',
  length:'由当前插件处理的MIME类型数量'
}]
```
- navigator.registerProtocolHandler()
可以借助这个方法将Web应用程序注册为像桌面软件一样的默认应用程序。  
必须传入3个参数：要处理的协议（如"mailto"或"ftp"）、处理该协议的URL，以及应用名称。

### screen对象
客户端显示器的信息，比如像素宽度和像素高度。
### history对象
history对象表示当前窗口首次使用以来用户的导航历史记录。  
- history.go(index of string)
```javascript
    // 后退一页
    history.go(-1);
    // 前进一页
    history.go(1);
    // 前进两页
    history.go(2);
    // 导航到最近的wrox.com页面
    history.go("wrox.com");
    // 导航到最近的nczonline.net页面
    history.go("nczonline.net");
    // 后退一页
    history.back();
    // 前进一页
    history.forward();
```
- history.length 这个属性反映了历史记录的数量，包括可以前进和后退的页面。
#### 历史状态管理
状态管理API则可以让开发者改变浏览器URL而不会加载新页面，history.pushState()方法。这个方法接收3个参数：一个state对象、一个新状态的标题和一个（可选的）相对URL。pushState()会创建新的历史记录，所以也会相应地启用“后退”按钮。单击“后退”按钮，就会触发window对象上的popstate事件。
## 十三、客户端检测
### 能力检测
又称特性检测，测试浏览器是否支持某个特性。例如检测浏览器是否支持getElementById：
```javascript
    function getElement(id) {
      if (document.getElementById) {
        return document.getElementById(id);
      } else if (document.all) {
        return document.all[id];
      } else {
        throw new Error("No way to retrieve element! ");
      }
    }
```
先检测最优方法，再检测备用方案，实在不行再抛错。
#### 安全能力检测
进行能力检测时应该尽量使用typeof操作符，但光有它还不够。尤其是某些宿主对象并不保证对typeof测试返回合理的值。
#### 基于能力检测进行浏览器分析
集中检测所有能力，而不是等到用的时候再重复检测。  
根据对浏览器特性的检测并与已知特性对比，确认用户使用的是什么浏览器。  
通过检测一种或一组能力，并不总能确定使用的是哪种浏览器。  
### 用户代理检测
- navigator.userAgent 用户代理检测通过浏览器的用户代理字符串确定使用的是什么浏览器。
- navigator.oscpu 对应用户代理字符串中操作系统/系统架构相关信息。
- navigator.vendor 包含浏览器开发商信息。
- navigator.platform 表示浏览器所在的操作系统。
- screen.colorDepth 和screen.pixelDepth返回一样的值，即显示器每像素颜色的位深。
- screen.orientation 包含Screen Orientation API定义的屏幕信息。orientation.type和angle可以确定屏幕是否旋转。
- navigator.geolocation 属性暴露了Geolocation API，可以让浏览器脚本感知当前设备的地理位置。
- navigator. onLine 可以确定浏览器的联网状态。连网和断网会触发window的online和offline事件。
- navigator.connection 网络连接状况。
- navigator.getBattery() 属性暴露了Battery API，可以让浏览器脚本感知当前设备的电池状态。
- navigator.hardwareConcurrency 返回浏览器支持的逻辑处理器核心数量
- navigator.deviceMemory 返回设备大致的系统内存大小
- navigator.maxTouchPoints 属性返回触摸屏支持的最大关联触点数量

## 十四、DOM
文档对象模型（DOM, Document Object Model）是HTML和XML文档的编程接口。
### 节点层级
任何HTML或XML文档都可以用DOM表示为一个由节点构成的层级结构。  
document节点表示每个文档的根节点。  
根节点的唯一子节点是html元素，我们称之为文档元素（documentElement）。  
```html
Document
  Element <html>
    Element <head>
      Element <title>
      Element <meta>
    Element <body>
      Element <p>
        Element <a>
          Element <img>
```
HTML中的每段标记都可以表示为这个树形结构中的一个节点。  
DOM中总共有12种节点类型，这些类型都继承一种基本类型。  
#### Node类型
在JavaScript中，所有节点类型都继承Node类型，因此所有类型都共享相同的基本属性和方法。  
每个节点都有nodeType属性，表示该节点的类型。节点类型由定义在Node类型上的12个数值常量表示： 
- Node.ELEMENT_NODE 元素节点 1
- Node.ATTRIBUTE_NODE 属性节点 2
- Node.TEXT_NODE 文本节点 3
- Node.CDATA_SECTION_NODE CDATA节点 4
- Node.ENTITY_REFERENCE_NODE 实体引用节点 5
- Node.ENTITY_NODE 实体节点 6
- Node.PROCESSING_INSTRUCTION_NODE 注释节点 7
- Node.COMMENT_NODE 注释节点 8
- Node.DOCUMENT_NODE 文档节点 9
- Node.DOCUMENT_TYPE_NODE 文档类型节点 10
- Node.DOCUMENT_FRAGMENT_NODE 文档片段节点 11
- Node.NOTATION_NODE 注释节点 12
nodeName与nodeValue保存着有关节点的信息。  
对元素而言，nodeName始终等于元素的标签名，而nodeValue则始终为null。  
每个节点都有一个childNodes属性，其中包含一个NodeList的实例,previousSibling和nextSibling可以在这个列表的节点间导航，firstChild和lastChild分别指向childNodes中的第一个和最后一个子节点。    
每个节点都有一个parentNode属性，指向其DOM树中的父元素。 
hasChildNodes()返回节点是否有子节点。  
##### 操作节点
appendChild() 方法将一个节点添加到父节点的末尾。 
insertBefore() 添加节点到开头。  
replaceChild()方法接收两个参数：要插入的节点和要替换的节点。要替换的节点会被返回并从文档树中完全移除，要插入的节点会取而代之。  
removeChild() 移除节点  
cloneNode(boolean)，会返回与调用它的节点一模一样的节点，传入一个布尔，代表是否深复制，深复制会复制节点上所有子节点。返回的节点没有父亲节点，可通过appendChild插入文档中。  
#### Document类型  
文档对象document是HTMLDocument的实例（HTMLDocument继承Document），表示整个HTML页面。  
- nodeType等于9；
- nodeName值为"#document"；
- nodeValue值为null；
- parentNode值为null；
- ownerDocument值为null；
- 子节点可以是DocumentType（最多一个）、Element（最多一个）、ProcessingInstruction或Comment类型。
- document.documentElement属性返回文档的根元素，即html标签。
- document.body 属性返回文档的body元素，即body标签。
- document.doctype 属性返回文档的doctype，即<!DOCTYPE>标签。
- document.title 当前页面的标题，可修改
- document.URL 当前页面的URL
- document.domain 域名，只能设置当前url包含的域名
- document.getElementById(id) 
- document.getElementsByTagName(img) 返回数组，所有img，可传入*，返回所有元素。
- document.getElementsByName(name) 通过元素的name属性，返回数组
- document.anchors包含文档中所有带name属性的a元素。
- document.forms包含文档中所有form元素（与document.getElementsByTagName ("form")返回的结果相同）。
- document.images包含文档中所有img元素（与document.getElementsByTagName ("img")返回的结果相同）。
- document.links包含文档中所有带href属性的a元素。

### Element类型
Element表示XML或HTML元素，对外暴露出访问元素标签名、子节点和属性的能力。Element类型的节点具有以下特征：
- nodeType等于1；
- nodeName值为元素的标签名；
- nodeValue值为null；
- parentNode值为Document或Element对象；
- 子节点可以是Element、Text、Comment、ProcessingInstruction、CDATASection、EntityReference类型。
可以通过nodeName或tagName属性来获取元素的标签名。注意大小写。  
所有HTML元素都通过HTMLElement类型表示，所有HTML元素都有以下属性：
- id，元素在文档中的唯一标识符；
- title，包含元素的额外信息，通常以提示条形式展示；
- lang，元素内容的语言代码（很少用）；
- dir，语言的书写方向（"ltr"表示从左到右，"rtl"表示从右到左，同样很少用）；
- className，相当于class属性，用于指定元素的CSS类（因为class是ECMAScript关键字，所以不能直接用这个名字）。
```html
    <div id="myDiv" class="bd" title="Body text" lang="en" dir="ltr"></div>
    <script>
          let div = document.getElementById("myDiv");
    alert(div.id);           // "myDiv"
    alert(div.className);   // "bd"
    alert(div.title);        // "Body text"
    alert(div.lang);         // "en"
    alert(div.dir);          // "ltr"
    </script>
```
可以直接通过元素来修改标签的内容。  
与属性相关的DOM方法主要有3个：getAttribute()、setAttribute()和removeAttribute()。这些方法主要用于操纵属性。属性名不区分大小写。  
```js
    let div = document.getElementById("myDiv");
    alert(div.getAttribute("id"));      // "myDiv"
    alert(div.getAttribute("class"));   // "bd"
    alert(div.getAttribute("title"));   // "Body text"
    alert(div.getAttribute("lang"));    // "en"
    alert(div.getAttribute("dir"));     // "ltr"
```
通过DOM对象访问的属性中有两个返回的值跟使用getAttribute()取得的值不一样：
- style DOM对象返回一个CSSStyleDeclaration对象，getAttribute()只返回字符串。
- onclick DOM对象返回一个函数，getAttribute()返回源码。
setAttribute(name,value)  
#### 创建元素
document.createElement(tag)

### Text类型
包含按字面解释的纯文本：
nodeType等于3；
- nodeName值为"#text"；
- nodeValue值为节点中包含的文本；
- parentNode值为Element对象；
- 不支持子节点。

### Comment类型
DOM中的注释通过Comment类型表示。
- nodeType等于8；
- nodeName值为"#comment"；
- nodeValue值为注释的内容；
- parentNode值为Document或Element对象；
- 不支持子节点。
### CDATASection类型
CDATASection类型表示XML中特有的CDATA区块。  nodeType等于4；
### DocumentType类型
DocumentType类型的节点包含文档的文档类型（doctype）信息，DocumentType对象保存在document.doctype属性中。
- nodeType等于10；
- nodeName值为文档类型的名称；
- nodeValue值为null；
- parentNode值为Document对象；
- 不支持子节点。
name这个属性包含文档类型的名称，即紧跟在`<! DOCTYPE`后面的那串文本。
### DocumentFragment类型

### DOM编程
#### 动态脚本
```js
    <script src="foo.js"></script>
    // 使用dom实现这个操作
    let script = document.createElement("script");
    script.src = "foo.js";
    document.body.appendChild(script);
```
还可以动态添加函数：
```js
    let script = document.createElement("script");
    script.appendChild(document.createTextNode("function sayHi(){alert('hi'); }"));
    document.body.appendChild(script);
```
#### 动态样式
使用DOM添加link
```js
    let link = document.createElement("link");
    link.rel = "stylesheet";
    link.type = "text/css";
    link.href = "styles.css";
    let head = document.getElementsByTagName("head")[0];
    head.appendChild(link);
```
使用DOM添加style
```js
    let style = document.createElement("style");
    style.type = "text/css";
    style.appendChild(document.createTextNode("body{background-color:red}"));
    let head = document.getElementsByTagName("head")[0];
    head.appendChild(style);
```
#### MutationObserver接口
可以在DOM被修改时异步执行回调。
```js
    let observer = new MutationObserver(() => console.log('<body> attributes changed'));
    observer.observe(document.body, { attributes: true });
```
- observe() 可复用  
使用observe方法把一个节点和一个回调函数绑定到一起。  
- disconnect() 终止所有监听
### 总结
DOM由一系列节点类型构成，主要包括以下几种。
- Node是基准节点类型，是文档一个部分的抽象表示，所有其他类型都继承Node。
- Document类型表示整个文档，对应树形结构的根节点。在JavaScript中，document对象是Document的实例，拥有查询和获取节点的很多方法。
- Element节点表示文档中所有HTML或XML元素，可以用来操作它们的内容和属性。
- 其他节点类型分别表示文本内容、注释、文档类型、CDATA区块和文档片段。

## 十五、DOM扩张
### Selectors API
- querySelector()  
querySelector()方法接收CSS选择符参数，返回匹配该模式的第一个后代元素。  
```js
        // 取得<body>元素
    let body = document.querySelector("body");
    // 取得ID为"myDiv"的元素
    let myDiv = document.querySelector("#myDiv");
    // 取得类名为"selected"的第一个元素
    let selected = document.querySelector(".selected");
    // 取得类名为"button"的图片
    let img = document.body.querySelector("img.button");
```
- querySelectorAll() 返回所有匹配的项，是个NodeList
- matches() 检查一个元素是否匹配指定的选择器
### 元素遍历
Element Traversal API为DOM元素添加了5个属性：
- childElementCount，返回子元素数量（不包含文本节点和注释）；
- firstElementChild，指向第一个Element类型的子元素（Element版firstChild）；
- lastElementChild，指向最后一个Element类型的子元素（Element版lastChild）；
- previousElementSibling，指向前一个Element类型的同胞元素（Element版previousSibling）；
- nextElementSibling，指向后一个Element类型的同胞元素（Element版nextSibling）。
### HTML5
- getElementsByClassName() 返回一个包含所有类名为className的元素的NodeList
- classList
```js
    // 删除"disabled"类
    div.classList.remove("disabled");
    // 添加"current"类
    div.classList.add("current");
    // 切换"user"类
    div.classList.toggle("user");
    // 检测类名
    if (div.classList.contains("bd") && ! div.classList.contains("disabled")){
      // 执行操作
    )
    // 迭代类名
    for (let class of div.classList){
      doStuff(class);
    }
```
- document.activeElement 返回当前活动元素
- document.hasFocus() 方法，该方法返回布尔值，表示文档是否拥有焦点
- document.readyState  loading，表示文档正在加载；complete，表示文档加载完成。
- document.compatMode 浏览器当前处于什么渲染模式。"CSS1Compat" or "BackCompat"
- document.head 指向文档的head元素
- document.characterSet = "UTF-8";
innerHTML:  
```js
div.innerHTML = "Hello & welcome, <b>\"reader\"! </b>";
// 插入div中
```
outerHTML：
```js
div.innerHTML = "Hello & welcome, <b>\"reader\"! </b>";
// 替换div
```
- scrollIntoView()方法存在于所有HTML元素上  
alignToTop 窗口滚动后元素的顶部是否与与视口顶部对齐  
scrollIntoViewOptions behavior：定义过渡动画，可取的值为"smooth"和"auto"，block：定义垂直方向的对齐，可取的值为"start"、"center"、"end"和"nearest"，inline：定义水平方向的对齐，可取的值为"start"、"center"、"end"和"nearest"

### 专有扩展
- children属性
- contains()方法
- innerText属性
- outerText属性
- scrollIntoViewIfNeeded()

## 十六、DOM2和DOM3
HTML中的样式有3种定义方式：外部样式表（通过link元素）、文档样式表（使用style元素）和元素特定样式（使用style属性）。  
通过DOM修改样式：
```js
    let myDiv = document.getElementById("myDiv");
    // 设置背景颜色
    myDiv.style.backgroundColor = "red";
    // 修改大小
    myDiv.style.width = "100px";
    myDiv.style.height = "200px";
    // 设置边框
    myDiv.style.border = "1px solid black";

    // cssText是一次性修改元素多个样式
    myDiv.style.cssText = "width: 25px; height: 100px; background-color: green";
```
以后再看吧。。。。

## 十七、事件
### 事件流
事件流描述了页面接收事件的顺序。  
#### 事件冒泡
被点击的元素，最先触发click事件。然后，click事件沿DOM树一路向上，在经过的每个节点上依次触发，直至到达document对象。
#### 事件捕获
在事件捕获中，click事件首先由document元素捕获，然后沿DOM树依次向下传播，直至到达实际的目标元素。
#### DOM事件流
事件流分为3个阶段：事件捕获、到达目标和事件冒泡。 
### 事件处理程序
为响应事件而调用的函数被称为事件处理程序（或事件监听器）。
#### HTML事件处理
以下列方式创建的事件处理程序，会创建一个函数封装属性的值：
```js
    function() {
      with(document) {
        with(this) {
          // 属性值
          console.log(this.value)
        }
      }
    }
```
onclick属性中的值能直接访问到document和this里面的值
```html
    <!-- 输出"Click Me" -->
    <input type="button" value="Click Me" onclick="console.log(this.value)">
```
这种方式的事件处理程序会创建一个局部变量event。this指向这个元素。  
如果这个元素是一个表单输入框，则作用域链中还会包含表单元素：
```js
      function() {
        with (document) {
          with (this.form) {
            with (this) {
              // 属性值
            }
          }
        }
      }
```
#### DOM0事件处理程序
```js
    let btn = document.getElementById("myBtn");
    btn.onclick = function() {
      console.log(this.id); // myBtn
      console.log(btn===this)  // true
    };
```
DOM0事件处理程序的this指向元素本身。不会包裹this和document。  
#### DOM2事件处理程序
addEventListener()和removeEventListener()
```js
    let btn = document.getElementById("myBtn");
    btn.addEventListener('click',function() {
      console.log(this.id); // myBtn
      console.log(btn===this)  // true
    },false); // true为捕获阶段触发，false非捕获阶段触发
```
可以为同一个元素添加多个事件。  
#### IE事件处理程序
attachEvent() 需要用'onclick' this = window
#### 跨浏览器事件处理程序
DOM2>IE>DOM1

### 事件对象
在DOM中发生事件时，所有相关信息都会被收集并存储在一个名为event的对象中。
#### DOM事件对象
event对象是传给事件处理程序的唯一参数。event.type属性包含的事件类型。  
在事件处理程序内部，this对象始终等于currentTarget的值，而target只包含事件的实际目标（触发事件的元素）。  
event.preventDefault()方法用于阻止特定事件的默认动作(比如啊标签的href)。 
event.stopPropagation()用于取消后续事件捕获或冒泡。  
event.eventPhase可以确定事件流的状态：1：捕获阶段，2目标调用，3冒泡阶段。
::: tip 注意
event对象只在事件处理程序执行期间存在，一旦执行完毕，就会被销毁。
:::
#### IE事件对象
DOM0方式指定的事件，event是window的一个属性。attachEvent()指定的，则event对象会作为唯一的参数传给处理函数，但仍是window的属性。
returnValue设置为false相当于preventDefault()
```js
    var link = document.getElementById("myLink");
    link.onclick = function() {
      window.event.returnValue = false;
    };
```
ancelBubble属性与DOM stopPropagation()方法用途一样，都可以阻止事件冒泡。  
```js
    var link = document.getElementById("myLink");
    link.onclick = function() {
      window.event.cancelBuddle = true;
    };
```
#### 跨浏览器事件对象

### 事件类型
DOM3 Events定义了如下事件类型:
- 用户界面事件（UIEvent）：涉及与BOM交互的通用浏览器事件。
- 焦点事件（FocusEvent）：在元素获得和失去焦点时触发。
- 鼠标事件（MouseEvent）：使用鼠标在页面上执行某些操作时触发。
- 滚轮事件（WheelEvent）：使用鼠标滚轮（或类似设备）时触发。
- 输入事件（InputEvent）：向文档中输入文本时触发。
- 键盘事件（KeyboardEvent）：使用键盘在页面上执行某些操作时触发。
- 合成事件（CompositionEvent）：在使用某种IME（InputMethod Editor，输入法编辑器）输入字符时触发。
#### 用户界面事件
- load：在window上当页面加载完成后触发，在窗套（frameset）上当所有窗格（frame）都加载完成后触发，在img元素上当图片加载完成后触发，在object元素上当相应对象加载完成后触发。
- unload：在window上当页面完全卸载后触发，在窗套上当所有窗格都卸载完成后触发，在object元素上当相应对象卸载完成后触发。
- abort：在object元素上当相应对象加载完成前被用户提前终止下载时触发。
- error：在window上当JavaScript报错时触发，在img元素上当无法加载指定图片时触发，在object元素上当无法加载相应对象时触发，在窗套上当一个或多个窗格无法完成加载时触发。
- select：在文本框（input或textarea）上当用户选择了一个或多个字符时触发。
- resize：在window或窗格上当窗口或窗格被缩放时触发。
- scroll：当用户滚动包含滚动条的元素时在元素上触发。body元素包含已加载页面的滚动条。
- unload：在文档卸载完成后触发，可以给body添加一个onunload事件，在页面卸载时执行一些操作。
- resize：当浏览器窗口被缩放到新高度或宽度时，会触发resize事件。
#### 焦点事件
焦点事件在页面元素获得或失去焦点时触发。
- blur：当元素失去焦点时触发。这个事件不冒泡，所有浏览器都支持。
- focus：当元素获得焦点时触发。这个事件不冒泡，所有浏览器都支持。
- focusin：当元素获得焦点时触发。这个事件是focus的冒泡版。
- focusout：当元素失去焦点时触发。这个事件是blur的通用版。
当焦点从页面中的一个元素移到另一个元素上时，会依次发生如下事件：
1. focuscout在失去焦点的元素上触发。
2. focusin在获得焦点的元素上触发。
3. blur在失去焦点的元素上触发。
4. focus在获得焦点的元素上触发。
#### 鼠标和滚轮事件
- click：在用户单击鼠标主键（通常是左键）或按键盘回车键时触发。这主要是基于无障碍的考虑，让键盘和鼠标都可以触发onclick事件处理程序。
- dblclick：在用户双击鼠标主键（通常是左键）时触发。这个事件不是在DOM2 Events中定义的，但得到了很好的支持，DOM3Events将其进行了标准化。
- mousedown：在用户按下任意鼠标键时触发。这个事件不能通过键盘触发。
- mouseenter：在用户把鼠标光标从元素外部移到元素内部时触发。这个事件不冒泡，也不会在光标经过后代元素时触发。mouseenter事件不是在DOM2 Events中定义的，而是DOM3Events中新增的事件。
- mouseleave：在用户把鼠标光标从元素内部移到元素外部时触发。这个事件不冒泡，也不会在光标经过后代元素时触发。mouseleave事件不是在DOM2 Events中定义的，而是DOM3Events中新增的事件。
- mousemove：在鼠标光标在元素上移动时反复触发。这个事件不能通过键盘触发。
- mouseout：在用户把鼠标光标从一个元素移到另一个元素上时触发。移到的元素可以是原始元素的外部元素，也可以是原始元素的子元素。这个事件不能通过键盘触发。
- mouseover：在用户把鼠标光标从元素外部移到元素内部时触发。这个事件不能通过键盘触发。
- mouseup：在用户释放鼠标键时触发。这个事件不能通过键盘触发。
- mousewheel：滚轮事件
除了mouseenter和mouseleave，所有鼠标事件都会冒泡，都可以被取消。  
click事件依赖mousedown和mouseup，dblclick依赖两次click，任意一个取消，都会导致不触发。    
DOM通过event对象的relatedTarget属性提供了相关元素的信息。这个属性只有在mouseover和mouseout事件发生时才包含值，其他所有事件的这个属性的值都是null。  
##### 鼠标坐标
- 窗口坐标：event对象的clientX和clientY属性中
- 页面坐标：通过event对象的pageX和pageY可以获取。在页面没有滚动时，pageX和pageY与clientX和clientY的值相同。
- 屏幕坐标：event对象的screenX和screenY属性获取鼠标光标在屏幕上的坐标。
##### 修饰键
Shift、Ctrl、Alt和Meta，事件对象中可以判断这几个键是否按下：shiftKey、ctrlKey、altKey和metaKey。
##### 鼠标按键
对mousedown和mouseup事件来说，event对象上会有一个button属性，表示按下或释放的是哪个按键。 
##### 触摸屏幕
- 不支持dblclick事件。双击浏览器窗口可以放大，但没有办法覆盖这个行为。
- 单指点触屏幕上的可点击元素会触发mousemove事件。如果操作会导致内容变化，则不会再触发其他事件。如果屏幕上没有变化，则会相继触发mousedown、mouseup和click事件。点触不可点击的元素不会触发事件。可点击元素是指点击时有默认动作的元素（如链接）或指定了onclick事件处理程序的元素。
- mousemove事件也会触发mouseover和mouseout事件。
- 双指点触屏幕并滑动导致页面滚动时会触发mousewheel和scroll事件。
#### 键盘与输入事件
键盘事件包含3个事件：
- keydown：在按键被按下时触发。
- keypress，用户按下键盘上某个键并产生字符时触发，而且持续按住会重复触发。Esc键也会触发这个事件。DOM3 Events废弃了keypress事件，而推荐textInput事件。
- keyup，用户释放键盘上某个键时触发。
输入事件只有一个，即textInput。textInput会在文本被插入到文本框之前触发。  
如果一个字符键被按住不放，keydown和keypress就会重复触发，直到这个键被释放。 
::: tip 注意
键盘事件支持与鼠标事件相同的修饰键。shiftKey、ctrlKey、altKey和metaKey属性在键盘事件中都是可用的。
:::
对于keydown和keyup事件，event对象的keyCode属性中会保存一个键码，对应键盘上特定的一个键。  
event对象上支持charCode属性，只有发生keypress事件时这个属性才会被设置值，包含的是按键字符对应的ASCII编码。可以使用String.fromCharCode()方法将其转换为实际的字符。  
DOM3 Events规范并未规定charCode属性，而是定义了key和char两个新属性。  
#### 合成事件
IME通常需要同时按下多个键才能输入一个字符。合成事件用于检测和控制这种输入。
#### HTML5事件
- contextmenu事件：在鼠标右键点击时触发。可以preventDefault()来阻止默认行为，然后添加自己想要的操作。
- beforeunload事件：给开发者提供阻止页面被卸载的机会。这个事件会向用户显示一个确认框，其中的消息表明浏览器即将卸载页面，并请用户确认是希望关闭页面，还是继续留在页面上。
```js
    window.addEventListener("beforeunload", (event) => {
      let message = "I'm really going to miss you if you go.";
      event.returnValue = message;
      return message;
    });
```
- DOMContentLoaded事件：DOM树构建完成后立即触发，而不用等待图片、JavaScript文件、CSS文件或其他资源加载完成。
- readystatechange事件：
- pageshow与pagehide事件：其会在页面显示时触发，无论是否来自往返缓存。来自往返缓存persisted为true。
- hashchange事件：用于在URL散列值（URL最后#后面的部分）发生变化时通知开发者。
#### 设备事件
- orientationchange事件：0表示垂直模式，90表示左转水平模式（主屏幕键在右侧）, -90表示右转水平模式（主屏幕键在左）。window.orientation可获取到信息。IOS
- deviceorientation事件 陀螺仪？
- devicemotion事件 移动
#### 触摸事件
- touchstart事件：触摸屏幕时触发。
- touchmove：手指在屏幕上滑动时连续触发。在这个事件中调用preventDefault()可以阻止滚动。
- touchend：手指从屏幕上移开时触发。
- touchcancel：系统停止跟踪触摸时触发。文档中并未明确什么情况下停止跟踪。
- touches: Touch对象的数组，表示当前屏幕上的每个触点。
- targetTouches: Touch对象的数组，表示特定于事件目标的触点。
- changedTouches: Touch对象的数组，表示自上次用户动作之后变化的触点。
##### 手势事件
- gesturestart：一个手指已经放在屏幕上，再把另一个手指放到屏幕上时触发。
- gesturechange：任何一个手指在屏幕上的位置发生变化时触发。
- gestureend：其中一个手指离开屏幕时触发。
每个手势事件的event对象都包含所有标准的鼠标事件属性：bubbles、cancelable、view、clientX、clientY、screenX、screenY、detail、altKey、shiftKey、ctrlKey和metaKey。  
新增的两个event对象属性是rotation和scale。rotation属性表示手指变化旋转的度数，负值表示逆时针旋转，正值表示顺时针旋转（从0开始）。scale属性表示两指之间距离变化（对捏）的程度。开始时为1，然后随着距离增大或缩小相应地增大或缩小。
#### 事件参考
一堆图。。。
### 内存与性能
在JavaScript中，页面中事件处理程序的数量与页面整体性能直接相关。
- 每个函数都是对象，都占用内存空间，对象越多，性能越差。
- 为指定事件处理程序所需访问DOM的次数会先期造成整个页面交互的延迟。 
#### 事件委托
事件委托利用事件冒泡，可以只使用一个事件处理程序来管理一种类型的事件。  
使用事件委托，只要给所有元素共同的祖先节点添加一个事件处理程序，就可以解决问题。 
事件委托具有如下优点:
- document对象随时可用，任何时候都可以给它添加事件处理程序（不用等待DOMContentLoaded或load事件）。这意味着只要页面渲染出可点击的元素，就可以无延迟地起作用。
- 节省花在设置页面事件处理程序上的时间。只指定一个事件处理程序既可以节省DOM引用，也可以节省时间。
- 减少整个页面所需的内存，提升整体性能。
##### 删除事件处理程序
事件处理程序越多，页面性能就越差。应该及时删除不用的事件处理程序。
1. 删除带有事件处理程序的元素，removeChild()或replaceChild()删除节点。innerHTML需要手动删除程序。
2. 在onunload事件处理程序中趁页面尚未卸载先删除所有事件处理程序。

### 模拟事件
#### DOM事件模拟
使用document.createEvent(event:string)方法创建一个event对象。  
- "UIEvents"（DOM3中是"UIEvent"）：通用用户界面事件（鼠标事件和键盘事件都继承自这个事件）。
- "MouseEvents"（DOM3中是"MouseEvent"）：通用鼠标事件。
- "HTMLEvents"（DOM3中没有）：通用HTML事件（HTML事件已经分散到了其他事件大类中）。
创建event对象-》初始化-》使用dispatchEvent()触发调用-》冒泡并触发事件处理程序执行
**模拟鼠标事件：**    
createEvent("MouseEvents")会返回一个event对象，对象有一个initMouseEvent()方法，接收很多参数。
```js
    let btn = document.getElementById("myBtn");
    // 创建event对象
    let event = document.createEvent("MouseEvents");
    // 初始化event对象
    // 要触发的事件类型、表示事件是否冒泡、表示事件是否可以取消、与事件关联的视图
    event.initMouseEvent("click", true, true, document.defaultView,
                          0, 0, 0, 0, 0, false, false, false, false, 0, null);
    // 触发事件
    btn.dispatchEvent(event);
```
**模拟键盘事件：**   
 createEvent("KeyboardEvent")会返回一个event对象，对象有一个initKeyboardEvent()方法。很多参数。。。
**模拟其他事件：**     
```js
    let event = document.createEvent("HTMLEvents");
    event.initEvent("focus", true, false);
    target.dispatchEvent(event);
```
**自定义DOM事件：**     
createEvent("CustomEvent")。返回的对象包含initCustomEvent()方法，该方法接收以下4个参数。 
- type（字符串）：要触发的事件类型，如"myevent"。
- bubbles（布尔值）：表示事件是否冒泡。
- cancelable（布尔值）：表示事件是否可以取消。
- detail（对象）：任意值。作为event对象的detail属性。
自定义事件可以像其他事件一样在DOM中派发，比如：
```js
    let div = document.getElementById("myDiv");
    div.addEventListener("myevent", (event) => {
      console.log("DIV: " + event.detail);
    });
    document.addEventListener("myevent", (event) => {
      console.log("DOCUMENT: " + event.detail);
    });
    if (document.implementation.hasFeature("CustomEvents", "3.0")) {
      event = document.createEvent("CustomEvent");
      event.initCustomEvent("myevent", true, false, "Hello world! ");
      div.dispatchEvent(event);
    }
```
**IE事件模拟：**   
考虑兼容性的话可以看看。。

## 十八、动画与Canvas图形
### 使用requestAnimationFrame
早期动画通过setInterval()和setTimeout()实现，但是时间不精准。  
#### requestAnimationFrame
requestAnimationFrame(fn,TimeStamp)
```js
    function updateProgress() {
      var div = document.getElementById("status");
      div.style.width = (parseInt(div.style.width, 10) + 5) + "%";
      if (div.style.left ! = "100%") {
      requestAnimationFrame(updateProgress);
      }
    }
    requestAnimationFrame(updateProgress);
```
#### cancelAnimationFrame
#### 通过requestAnimationFrame节流

### 基本的画布功能
出现在开始和结束标签之间的内容是后备数据，会在浏览器不支持canvas元素时显示。
```html
<canvas id="drawing" width="200" height="200">A drawing of something.</canvas>
```
width和height属性也可以在DOM节点上设置，因此可以随时修改。整个元素还可以通过CSS添加样式，并且元素在添加样式或实际绘制内容前是不可见的。  
要在画布上绘制图形，首先要取得绘图上下文。  
```js
    let drawing = document.getElementById("drawing");
    // 确保浏览器支持<canvas>
    if (drawing.getContext) {
      let context = drawing.getContext("2d");
      // 其他代码
    }
    drawing.toDataURL('image/png') // 导出一张PNG格式的图片
```
### 2D绘图上下文
2D上下文的坐标原点(0, 0)在canvas元素的左上角。所有坐标值都相对于该点计算，因此x坐标向右增长，y坐标向下增长。默认情况下，width和height表示两个方向上像素的最大值。  
**1. 填充和描边**  
填充以指定样式（颜色、渐变或图像）自动填充形状，而描边只为图形边界着色。  
- 填充: fillStyle 字符串、渐变对象或图案对象CSS颜色值
- 描边: strokeStyle 字符串、渐变对象或图案对象CSS颜色值
```js
    let drawing = document.getElementById("drawing");
    // 确保浏览器支持<canvas>
    if (drawing.getContext) {
      let context = drawing.getContext("2d");
      context.strokeStyle = "red";
      context.fillStyle = "#0000ff";
    }
```
**2. 绘制矩形**   
矩形是唯一一个可以直接在2D绘图上下文中绘制的形状。
- fillRect(x,y,width,height)方法用于以指定颜色在画布上绘制并填充矩形。填充的颜色使用fillStyle属性指定。
- strokeRect(x,y,width,height)方法使用通过strokeStyle属性指定的颜色绘制矩形轮廓。
- lineWidth 描边宽度
- lineCap 线条端点的形状 ［"butt"（平头）、"round"（出圆头）或"square"（出方头）］
- lineJoin 线条交点的形状［"round"（圆转）、"bevel"（取平）或"miter"（出尖）］
- clearRect() 擦除画布中某个区域用于把绘图上下文中的某个区域变透明。通过先绘制形状再擦除指定区域。 

**3. 绘制路径**  
必须首先调用beginPath()方法以表示要开始绘制新路径。然后，再调用下列方法来绘制路径。  
- arc(x, y, radius, startAngle, endAngle, counterclockwise)：以坐标(x, y)为圆心，以radius为半径绘制一条弧线，起始角度为startAngle，结束角度为endAngle（都是弧度）。最后一个参数counterclockwise表示是否逆时针计算起始角度和结束角度（默认为顺时针）。
- arcTo(x1, y1, x2, y2, radius)：以给定半径radius，经由(x1, y1)绘制一条从上一点到(x2, y2)的弧线。
- bezierCurveTo(c1x, c1y, c2x, c2y, x, y)：以(c1x, c1y)和(c2x,c2y)为控制点，绘制一条从上一点到(x, y)的弧线（三次贝塞尔曲线）。
- lineTo(x, y)：绘制一条从上一点到(x, y)的直线。
- moveTo(x, y)：不绘制线条，只把绘制光标移动到(x, y)。
- quadraticCurveTo(cx, cy, x, y)：以(cx, cy)为控制点，绘制一条从上一点到(x, y)的弧线（二次贝塞尔曲线）。
- rect(x, y, width, height)：以给定宽度和高度在坐标点(x, y)绘制一个矩形。这个方法与strokeRect()和fillRect()的区别在于，它创建的是一条路径，而不是独立的图形。
创建路径之后,可用closePath()方法绘制一条返回起点的线。fillStyle属性并调用fill()方法来填充路径，也可以指定strokeStyle属性并调用stroke()方法来描画路径，还可以调用clip()方法基于已有路径创建一个新剪切区域。  
- isPointInPath(x,y) 确定点是否在路径上
**4. 绘制文本**  
fillText()和strokeText()，4个参数：要绘制的字符串、x坐标、y坐标和可选的最大像素宽度。  
- font：以CSS语法指定的字体样式、大小、字体族等，比如"10pxArial"。
- textAlign：指定文本的对齐方式，可能的值包括"start"、"end"、"left"、"right"和"center"。推荐使用"start"和"end"，不使用"left"和"right"，因为前者无论在从左到右书写的语言还是从右到左书写的语言中含义都更明确。
- textBaseLine：指定文本的基线，可能的值包括"top"、"hanging"、"middle"、"alphabetic"、"ideographic"和"bottom"。
- measureText(text) 返回text的width 
**5. 变换**  
改变绘制上下文的变换矩阵。
- rotate(angle)：围绕原点把图像旋转angle弧度。
- scale(scaleX, scaleY)：通过在x轴乘以scaleX、在y轴乘以scaleY来缩放图像。scaleX和scaleY的默认值都是1.0。
- translate(x, y)：把原点移动到(x, y)。执行这个操作后，坐标(0,0)就会变成(x, y)。
- transform(m1_1, m1_2, m2_1, m2_2, dx, dy)：像下面这样通过矩阵乘法直接修改矩阵。
- setTransform(m1_1, m1_2, m2_1, m2_2, dx, dy)：把矩阵重置为默认值，再以传入的参数调用transform()。
- save() 调用这个方法后，所有这一时刻的设置会被放到一个暂存栈中。
- restore() 这个方法会从暂存栈中取出并恢复之前保存的设置。
save()方法只保存应用到绘图上下文的设置和变换，不保存绘图上下文的内容。
**6. 绘制图像**  
- drawImage(image/canvas,x,y,width,height)
```js
    let image = document.images[0];
    context.drawImage(image, 10, 10);
```
还可以绘制一部分到画布上：  
drawImage(image,x,y,width,height,img-x,img-y,img-width,img-height)

**7. 阴影**  
- shadowColor: CSS颜色值，表示要绘制的阴影颜色，默认为黑色。
- shadowOffsetX：阴影相对于形状或路径的x坐标的偏移量，默认为0。
- shadowOffsetY：阴影相对于形状或路径的y坐标的偏移量，默认为0。
- shadowBlur：像素，表示阴影的模糊量。默认值为0，表示不模糊。

**8. 渐变**  
线性渐变：createLinearGradient(起点xy，终点xy)
```js
    let gradient = context.createLinearGradient(30, 30, 70, 70);
    gradient.addColorStop(0, "white");
    gradient.addColorStop(1, "black");
    // 绘制红色矩形
    context.fillStyle = "#ff0000";
    context.fillRect(10, 10, 50, 50);
    // 绘制渐变矩形
    context.fillStyle = gradient
    context.fillRect(30, 30, 50, 50);
```
放射渐变：createRadialGradient(起点xyr，终点xyr)
**9. 图案**  
createPattern(img,string) 第二个参数的值与CSS的background-repeat属性是一样的，包括"repeat"、"repeat-x"、"repeat-y"和"no-repeat"。

**10. 图像数据**  
getImageData(x,y,width,height)要从(x, y)开始取得width像素宽、height像素高的区域对应的数据。  

**11. 合成**  
globalAlpha属性：透明度 0-1  
globalCompositionOperation属性表示新绘制的形状如何与上下文中已有的形状融合。  
有很多选项，用到的时候可以查。 

### WebGL
WebGL是画布的3D上下文。  
```js
document.getElementById('cavans').getContext('webgl')
```
## 十九、表单脚本
### 表单基础
表单在HTML中以form元素表示，在JavaScript中则以HTMLFormElement类型表示。  
```js
    let form = document.getElementById("form1");
    // 取得页面中的第一个表单
    let firstForm = document.forms[0];
    // 取得名字为"form2"的表单
    let myForm = document.forms["form2"];
```
#### 提交表单
```html
    <!-- 通用提交按钮 -->
    <input type="submit" value="Submit Form">
    <!-- 自定义提交按钮 -->
    <button type="submit">Submit Form</button>
    <!-- 图片按钮 -->
    <input type="image" src="graphic.gif">
```
如果表单中有上述任何一个按钮，且焦点在表单中某个控件上，则按回车键也可以提交表单。  
也可以直接通过js提交
```js
    let form = document.getElementById("myForm");
    //提交表单
    form.submit()
```
#### 重置表单
```html
    <!-- 通用重置按钮 -->
    <input type="reset" value="Reset Form">
    <!-- 自定义重置按钮 -->
    <button type="reset">Reset Form</button>
```
也可以直接通过js重制
#### 表单字段
所有表单元素都是表单elements属性（元素集合）中包含的一个值，可以通过索引位置和name属性来访问。
```js
    let form = document.getElementById("form1");
    // 取得表单中的第一个字段
    let field1 = form.elements[0];
    // 取得表单中名为"textbox1"的字段
    let field2 = form.elements["textbox1"];
    // 取得字段的数量
    let fieldCount = form.elements.length;
```
- 表单字段的公共属性：disabled、form、name、readOnly、tabIndex、 type、value
- 表单字段的公共方法：focus()和blur()，HTML5为表单字段增加了autofocus属性，支持的浏览器会自动为带有该属性的元素设置焦点。
- 表单字段的公共事件：blur、change、focus
### 文本框编程
单行文本input，多行文本textarea。
**input**  
- size：文本框宽度，以字符数衡量
- value：文本框初始值
- maxLength：最多字符数
**textarea**  
- rows：文本框高度，以字符数衡量
- cols：文本框宽度，类似于<input>元素的size属性
- 与<input>不同的是，<textarea>的初始值必须包含在<textarea>和</textarea>之间
#### 选择文本
select()方法，用于全部选中文本框中的文本。  
select事件，select事件会在用户选择完文本后立即触发。
```js
    function getSelectedText(textbox){
      return textbox.value.substring(textbox.selectionStart,
                                      textbox.selectionEnd);
    }
```
setSelectionRange(begin,end)  选择部分文本。  
#### 输入过滤
有些输入框需要出现或不出现特定字符，可以通过阻止keypress的默认行为来屏蔽非数字字符。
处理剪贴板：beforecopy、copy、beforecut、cut、beforepaste、paste  
剪贴板上的数据可以通过window对象（IE）或event对象（Firefox、Safari和Chrome）上的clipboardData对象来获取。clipboardData对象上有3个方法：getData()、setData()和clearData()。  
#### 自动切换
通过focus实现
#### HTML5约束验证API
- required 必填
- type值增加"email"和"url"
- 输入元素 "number"、"range"、"datetime"、"datetime-local"、"date"、"month"、"week"和"time"
- min max step(步长)
- stepUp()和stepDown() 要从当前值加上或减去的数值。
- pattern 用于指定一个正则表达式
- checkValidity() 检查字段是否有效
- validity属性 返回一系列布尔值，检查每一个条件
- novalidate禁用验证 js中可以使用noValidate
- formnovalidate/formNoValidate 整个form禁用验证

### 选择框编程
选择框是使用select和option元素创建的。
- add(newOption, relOption)：在relOption之前向控件中添加新的option。
- multiple：布尔值，表示是否允许多选，等价于HTML的multiple属性。
- options：控件中所有option元素的HTMLCollection。
- remove(index)：移除给定位置的选项。
- selectedIndex：选中项基于0的索引值，如果没有选中项则为-1。对于允许多选的列表，始终是第一个选项的索引。
- size：选择框中可见的行数，等价于HTML的size属性。
option元素存在以下属性：
- index：选项在options集合中的索引。
- label：选项的标签，等价于HTML的label属性。
- selected：布尔值，表示是否选中了当前选项。把这个属性设置为true会选中当前选项。
- text：选项的文本。
- value：选项的值（等价于HTML的value属性）。

### 表单序列化
### 富文本编辑

## 二十、JavaScriptAPI
### Atomics与SharedArrayBuffer
看完27再回来看这个
### 跨上下文消息
跨文档消息(XDM)，是一种在不同执行上下文（如不同工作线程或不同源的页面）间传递信息的能力。  
XDM的核心是postMessage()方法。把数据传送到另一个位置。  
postMessage()方法接收3个参数：消息、表示目标接收源的字符串和可选的可传输对象的数组。  
接收到XDM消息后，window对象上会触发message事件，event包含下面三个信息：
- data：作为第一个参数传递给postMessage()的字符串数据。
- origin：发送消息的文档源，例如"http://www.wrox.com"。
- source：发送消息的文档中window对象的代理。这个代理对象主要用于在发送上一条消息的窗口中执行postMessage()方法。如果发送窗口有相同的源，那么这个对象应该就是window对象。
### Encoding API
Encoding API主要用于实现字符串与定型数组之间的转换。
### File API与Blob API
File API与Blob API是为了让Web开发者能以安全的方式访问客户端机器上的文件，从而更好地与这些文件交互而设计的。
### 媒体元素
迫使用Flash以便达到最佳的跨浏览器兼容性。HTML5新增了两个与媒体相关的元素，即audio和video，从而为浏览器提供了嵌入音频和视频的统一解决方案。  
### 原生拖放
在某个元素被拖动时，会（按顺序）触发以下事件：
1. dragstart
2. drag
3. dragend
在把元素拖动到一个有效的放置目标上时，会依次触发以下事件：  
1. dragenter
2. dragover
3. dragleave或drop
dropEffect属性可以告诉浏览器允许哪种放置行为。这个属性有以下4种可能的值：
- "none"：被拖动元素不能放到这里。这是除文本框之外所有元素的默认值。
- "move"：被拖动元素应该移动到放置目标。
- "copy"：被拖动元素应该复制到放置目标。
- "link"：表示放置目标会导航到被拖动元素（仅在它是URL的情况下）。


HTML5在所有HTML元素上规定了一个draggable属性，表示元素是否可以拖动。  

### Notifications API
Notifications API用于向用户显示通知。  
页面可以使用全局对象Notification向用户请求通知权限。这个对象有一个requestPemission()方法，该方法返回一个期约，用户在授权对话框上执行操作后这个期约会解决。  
```js
    new Notification('Title text! ',{
      body: 'text',
      image: 'image',
      vibrate: true
    });
```
close()方法可以关闭显示的通知。  
通知生命周期回调: 
- onshow在通知显示时触发；
- onclick在通知被点击时触发；
- onclose在通知消失或通过close()关闭时触发；
- onerror在发生错误阻止通知显示时触发。

### Page Visibility API
Page Visibility API旨在为开发者提供页面对用户是否可见的信息。
- document.visibilityState:"hidden"/"visible"/"prerender"
- visibilitychange事件 显示状态发生变化触发  
- document.hidden 页面是否隐藏

### Streams API
大块数据可能需要分小部分处理。 
#### 流
Stream API定义了三种流：
**可读流**：可以通过某个公共接口读取数据块的流。数据在内部从底层源进入流，然后由消费者（consumer）进行处理。  
**可写流**：可以通过某个公共接口写入数据块的流。生产者（producer）将数据写入流，数据在内部传入底层数据槽（sink）。  
**转换流**：由两种流组成，可写流用于接收数据（可写端），可读流用于输出数据（可读端）。这两个流之间是转换程序（transformer），可以根据需要检查和修改流内容。  
流的基本单位是块。
- 可读流
```js
let array = [1, 2, 3, 4, 5]
const readableStream = new ReadableStream({
  start(controller) {
    for (let chunk of array) {
      controller.enqueue(chunk)
    }
    controller.close()
  }
})
const readableStreamDefaultReader = readableStream.getReader()
for (let i = 0; i < 5; i++) {
  readableStreamDefaultReader.read().then(console.log)
}
// 1 2 3 4 5
```
- 可写流
```js
const writableStream = new WritableStream({
  write(value) {
    console.log(value)
  }
})
const writableStreamDefaultWriter = writableStream.getWriter()     
writableStreamDefaultWriter.write(1)
writableStreamDefaultWriter.close()
```
- 转换流
```js
  const { writable, readable } = new TransformStream({
    transform(chunk, controller) {
      controller.enqueue(chunk * 2)
    }
  })
  const readableStreamDefaultReader = readable.getReader()
  const writableStreamDefaultWriter = writable.getWriter()
```
#### 通过管道连接流
使用pipeThrough()方法把ReadableStream接入TransformStream。  
```js
const readableStream = new ReadableStream({
  start(controller) {
    controller.enqueue(1)
    controller.close()
  }
})
const transformStream = new TransformStream({
  transform(chunk, controller) {
    controller.enqueue(chunk * 2)
  }
})
// 通过管道连接流
const pipedStream = readableStream.pipeThrough(transformStream)
// 从连接流的输出获得读取器
const pipedStreamDefaultReader = pipedStream.getReader()
console.log(pipedStreamDefaultReader.read())
```
pipeTo()方法也可以将ReadableStream连接到WritableStream。
```js
const readableStream = new ReadableStream({
  start(controller) {
    controller.enqueue(1)
    ontroller.close()
  }
})
const writableStream = new WritableStream({
  write(value) {
    console.log(value)
  }
})
const pipeStream = readableStream.pipeTo(writableStream)
```
### 计时API
- window.performance.now() 这个方法返回一个微秒精度的浮点值。
- window.performance.timeOrigin 属性返回计时器初始化时全局系统时钟的值。
1. User Timing API用于记录和分析自定义性能条目。  
2. Navigation Timing API提供了高精度时间戳，用于度量当前页面加载速度。
3. Resource Timing API提供了高精度时间戳，用于度量当前页面加载时请求资源的速度。  
### Web组件
#### HTML模板
template标签的内容不属于活动文档，标签中的内容不会被渲染到页面上。而是存在于一个包含在HTML模板中的DocumentFragment节点内。DocumentFragment也是批量向HTML中添加元素的高效工具，可以给DocumentFragment添加完所有子节点，再一次性放入HTML中。  
如果想要复制模板，可以使用importNode()方法克隆DocumentFragment。  
```html
<body>
  <div id="foo">222</div>
  <template id="bar">
    <div>121212</div>
  </template>
</body>
<script>
  const fooElement = document.querySelector('#foo')
  const barTemplate = document.querySelector('#bar')
  const barFragment = barTemplate.content
  fooElement.appendChild(barFragment)
</script>
```
#### 影子DOM
影子DOM是通过attachShadow()方法创建并添加给有效HTML元素的。  
影子DOM的内容会实际渲染到页面上，而HTML模板的内容不会。CSS样式和CSS选择符可以限制在影子DOM子树而不是整个顶级DOM树中。  
通过slot标签可以用来放置原来的html：
```html
<div id="foo">
  <p>Foo</p>
</div>
<script>
  document
    .querySelector('div')
    .attachShadow({ mode: 'open' })
    .innerHTML = `
    <div id="bar">
      <slot></slot> 
    </div>             
    `
</script>
```
上面是默认槽位的例子，还可以使用命名槽位实现多个投射，通过匹配的slot/name属性对实现。
```html
<body>
  <div id="foo">
    <p slot="foo">Foo</p>
  </div>
  <template id="bar">
    <slot name="foo"></slot>
  </template>
</body>
<script>
  let foo = document.querySelector('#foo')
  let bar = document.querySelector('#bar')
  foo.attachShadow({ mode: 'open' }).innerHTML = bar.innerHTML
</script>
```
### 自定义元素
调用customElements.define()方法可以创建自定义元素。 
```js
class CustomElement extends HTMLElement {
  constructor() {
    super()
    console.log(1212)
  }
}
customElements.define('custom-tag',CustomElement)
<custom-tag></custom-tag> // 1212
```
如果自定义元素继承了一个元素类，那么可以使用is属性和extends选项将标签指定为该自定义元素的实例：
```js
class CustomElement extends HTMLDivElement {
  constructor() {
    super()
    console.log(1212)
  }
}
customElements.define('custom-tag',CustomElement,{extends:'div'})
<div is="custom-tag"></div> // 1212
```
每次将自定义元素添加到DOM中都会调用其类构造函数，所以很容易自动给自定义元素添加子DOM内容:
```js
class CustomElement extends HTMElement {
  constructor() {
    super()
    this.attachShadow({ mode: 'open' })
    this.shadowRoot.innerHTML = `
      <p>hello</p>
    `
    // 如果自定义元素内部有插槽，可以使用appendChild防止innerHTML覆盖插槽
  }
}
```
**自定义元素的声明周期：**    
- constructor()：在创建元素实例或将已有DOM元素升级为自定义元素时调用。
- connectedCallback()：在每次将这个自定义元素实例添加到DOM中时调用。
- disconnectedCallback()：在每次将这个自定义元素实例从DOM中移除时调用。
- attributeChangedCallback()：在每次可观察属性的值发生变化时调用。在元素实例初始化时，初始值的定义也算一次变化。
- adoptedCallback()：在通过document.adoptNode()将这个自定义元素实例移动到新文档对象时调用。
**反射自定义元素属性：**  
修改DOM和js对象应该能够互相反射。
```js
  class CustomElement extends HTMLElement {
    static get observedAttributes() {
      console.log(1212)
      return ['attr']
    }
    get attr() {
      return this.getAttribute('attr')
    }
    set attr(value) {
      this.setAttribute('attr', value)
    }
    attributeChangedCallback(name, oldValue, newValue) {
      if (newValue == oldValue) return
      this[name] = newValue
    }
  }
  customElements.define('custom-tag', CustomElement)
  let custom = document.createElement('custom-tag')
  document.body.appendChild(custom)
  custom.setAttribute('attr', false)
```
如果自定义元素已经有定义，那么CustomElementRegistry.get()方法会返回相应自定义元素的类。类似地，CustomElementRegistry.whenDefined()方法会返回一个期约，当相应自定义元素有定义之后解决。如果想在元素连接到DOM之前强制升级，可以使用CustomElementRegistry.upgrade()方法。  
### Web Cryptography API
#### 生成随机数
Math.random()是伪随机数生成器（PRNG），用于快速计算看起来随机的值，不适合加密。  
密码学安全伪随机数生成器（CSPRNG），crypto.getRandomValues()
```js
const array = new Uint8Array(2)
console.log(crypto.getRandomValues(array))
```
#### 使用SubtleCrypto对象
crypto.subtle包含一组方法，用于执行常见的密码学功能，如加密、散列、签名和生成密钥。因为所有密码学操作都在原始二进制数据上执行，所以SubtleCrypto的每个方法都要用到ArrayBuffer和ArrayBufferView类型。
以后可以看看。。。

## 二十一、错误处理与调试
### 错误处理
#### try/catch语句
```js
    try {
      // 可能出错的代码
    } catch (error) {
      // 出错时要做什么
    } finally {

    }
```
try/catch语句中可选的finally子句始终运行。
**错误类型：**ECMA-262定义了以下8种错误类型：  
1. Error是基类型，其他错误类型继承该类型。主要用于开发者抛出自定义错误。
2. InternalError类型的错误会在底层JavaScript引擎抛出异常时由浏览器抛出。例如，递归过多导致了栈溢出。  
3. EvalError类型的错误会在使用eval()函数发生异常时抛出。
4. RangeError错误会在数值越界时抛出。
5. ReferenceError会在找不到对象时发生。
6. SyntaxError经常在给eval()传入的字符串包含JavaScript语法错误时发生。
7. TypeError在JavaScript中很常见，主要发生在变量不是预期类型，或者访问不存在的方法时。
8. URIError，只会在使用encodeURI()或decodeURI()但传入了格式错误的URI时发生。

#### 抛出错误
```js
    throw 12345;
    throw "Hello world! ";
    throw true;
    throw { name: "JavaScript" };
    throw new Error("Something bad happened.");
    throw new SyntaxError("I don't like your syntax.");
    throw new InternalError("I can't do that, Dave.");
    throw new TypeError("What type of variable do you take me for? ");
    throw new RangeError("Sorry, you just don't have the range.");
    throw new EvalError("That doesn't evaluate.");
    throw new URIError("Uri, is that you? ");
    throw new ReferenceError("You didn't cite your references properly.");
```
使用throw操作符时，代码立即停止执行，除非try/catch语句捕获了抛出的值。通过继承Error可以创建自定义错误类型：
```js
    class CustomError extends Error {
      constructor(message) {
        super(message);
        this.name = "CustomError";
        this.message = message;
      }
    }
    throw new CustomError("My message");
```
#### error事件
任何没有被try/catch语句处理的错误都会在window对象上触发error事件。
```js 
    window.onerror = (message, url, line) => {
      console.log(message);
      return false // 不会抛出错误
    };
```
#### 识别错误
- 类型转换错误
- 数据类型错误
- 通信错误
##### 静态代码分析器
静态代码分析器要求使用类型、函数签名及其他指令来注解JavaScript，以此描述程序如何在基本可执行代码之外运行。分析器会比较注解和JavaScript代码的各个部分，对在实际运行时可能出现的潜在不兼容问题给出提醒。

### 调试技术
#### 把消息记录到控制台
console有如下方法：
- error（message）：在控制台中记录错误消息。
- info（message）：在控制台中记录信息性内容。
- log（message）：在控制台记录常规消息。
-  warn（message）：在控制台中记录警告消息。
#### 理解控制台运行时
在开发者工具的Element（元素）标签页内，单击DOM树中一个节点，就可以在Console（控制台）标签页中使用$0引用该节点的JavaScript实例。
#### 使用JavaScript调试器
debugger关键字，用于调用可能存在的调试功能。

### 旧版IE的常见错误
- 无效字符：在检测到JavaScript文件中存在无效字符时，IE会抛出"invalidcharacter"错误。
- 未找到成员：
- 未知运行时错误：
- 语法错误
- 系统找不到指定资源

## 二十二、处理XML

## 二十三、JSON
JavaScript对象简谱（JSON, JavaScript Object Notation）
### 语法
JSON语法支持表示3种类型的值。
- 简单值：字符串、数值、布尔值和null可以在JSON中出现，就像在JavaScript中一样。特殊值undefined不可以。
- 对象：第一种复杂数据类型，对象表示有序键/值对。每个值可以是简单值，也可以是复杂类型。
- 数组：第二种复杂数据类型，数组表示可以通过数值索引访问的值的有序列表。数组的值可以是任意类型，包括简单值、对象，甚至其他数组。
JSON中的对象必须使用双引号把属性名包围起来。  
### 解析与序列化
- JSON.stringify(json,['name','key']/function,space)  
第一个参数是要序列化的对象，第二个参数是一个数组，传入要序列化的属性。第二个参数也可以是一个函数，函数接收key和value两个参数，可以返回修改后的值。第三个参数控制缩进和空格，传入int表示缩进的空格数，还可以传换行符，传入字符串将使用这个字符串来缩进。  
在对象中实现toJSON方法并返回一个值，可以代替JSON.stringify()的结果。  
- JSON.parse(string,function)  
第一个参数传入要解析的字符串，第二个参数是替代函数，函数接收key/value，返回值将替换value，如果还原函数返回undefined，则结果中就会删除相应的键。

## 二十四、网络请求与远程资源
Ajax（Asynchronous JavaScript and XML，即异步JavaScript加XML）的技术。  
把Ajax推到历史舞台上的关键技术是XMLHttpRequest（XHR）对象。  
### XMLHttpRequest对象
#### 使用XHR
```js
let xhr = new XMLHttpRequest()
xhr.open('get',url,false)
xhr.send(body)
```
open()方法接收三个参数，请求方式，url还有是否异步。  
::: tip 注意
只能访问同源URL，也就是域名相同、端口相同、协议相同。如果请求的URL与发送请求的页面在任何方面有所不同，则会抛出安全错误。
:::
send方法接收一个参数，是作为请求体发送的数据。  
如果发送的请求是同步的，那么js会等待服务器响应后继续执行，xhr对象的以下属性会被填充数据：  
- responseText：作为响应体返回的文本。
- responseXML：如果响应的内容类型是"text/xml"或"application/xml"，那就是包含响应数据的XMLDOM文档。
- status：响应的HTTP状态。
- statusText：响应的HTTP状态描述。
在发送异步请求时，XHR对象有一个readyState属性，表示当前处在请求/响应过程的哪个阶段。这个属性有如下可能的值：  
- 0：未初始化（Uninitialized）。尚未调用open()方法。
- 1：已打开（Open）。已调用open()方法，尚未调用send()方法。
- 2：已发送（Sent）。已调用send()方法，尚未收到响应。
- 3：接收中（Receiving）。已经收到部分响应。
- 4：完成（Complete）。已经收到所有响应，可以使用了。
每次readyState从一个值变成另一个值，都会触发readystatechange事件。为保证跨浏览器兼容，onreadystatechange事件处理程序应该在调用open()之前赋值。
```js
    let xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
          alert(xhr.responseText);
        } else {
          alert("Request was unsuccessful: " + xhr.status);
        }
      }
    };
    xhr.open("get", "example.txt", true);
    xhr.send(null);
```
在收到响应之前如果想取消异步请求，可以调用xhr.abort()方法。

#### HTTP头部
默认情况下，XHR请求会发送以下头部字段：
- Accept：浏览器可以处理的内容类型。
- Accept-Charset：浏览器可以显示的字符集。
- Accept-Encoding：浏览器可以处理的压缩编码类型。
- Accept-Language：浏览器使用的语言。
- Connection：浏览器与服务器的连接类型。
- Cookie：页面中设置的Cookie。
- Host：发送请求的页面所在的域。
- Referer：发送请求的页面的URI。注意，这个字段在HTTP规范中就拼错了，所以考虑到兼容性也必须将错就错。（正确的拼写应该是Referrer。）
- User-Agent：浏览器的用户代理字符串。
如果需要发送额外的请求头部，可以使用setRequestHeader()方法。这个方法接收两个参数：头部字段的名称和值。必须在open()之后、send()之前调用setRequestHeader()：
```js
    let xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
          alert(xhr.responseText);
        } else {
          alert("Request was unsuccessful: " + xhr.status);
        }
      }
    };
    xhr.open("get", "example.php", true);
    xhr.setRequestHeader('key','value')
```
- getResponseHeader(name) 获取队形头部信息
- getAllResponseHeaders() 获取所有头部信息

#### GET请求
用于向服务器查询某些信息。
```js
  xhr.open("get", "example.php?name1=value1&name2=value2", true);
```
#### POST请求
用于向服务器发送应该保存的数据，POST请求都应该在请求体中携带提交的数据。
- Content-Type头部设置为"application/x-www-formurlencoded" 可以模拟表单提交
::: tip 注意
POST请求相比GET请求要占用更多资源。从性能方面说，发送相同数量的数据，GET请求比POST请求要快两倍。
:::
#### XMLHttpRequest Level 2
新增**FormData**类型，可以发送form表单：
```js
let xhr = new XMLHttpRequest();
xhr.open("post", "example.php", true);
let form = document.getElementById('form');
xhr.send(new FormDate(form));
```
**超时：**  
```js
let xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {}
xhr.open("get", "example.php", true);
xhr.timeout = 1000;
xhr.ontimeout = function() {
  alert("请求超时");
}
xhr.send(null);
```
超时之后仍会触发onreadystatechange事件，readyState为4，但是访问status会报错。
**overrideMimeType()方法：**
overrideMimeType()方法用于重写XHR响应的MIME类型。
```js
xhr.overrideMimeType('text/xml')
```
### 进度事件
6个进度相关的事件: 
- loadstart：在接收到响应的第一个字节时触发。
- progress：在接收响应期间反复触发。
- error：在请求出错时触发。
- abort：在调用abort()终止连接时触发。
- load：在成功接收完响应时触发。
- loadend：在通信完成时，且在error、abort或load之后触发。
每次请求都会首先触发loadstart事件，之后是一个或多个progress事件，接着是error、abort或load中的一个，最后以loadend事件结束。
#### progress事件
每次触发时，onprogress事件处理程序都会收到event对象，其target属性是XHR对象，且包含3个额外属性：
- lengthComputable是一个布尔值，表示进度信息是否可用；
- position是接收到的字节数；
- totalSize是响应的Content-Length头部定义的总字节数。

### 跨源资源共享
跨源资源共享（CORS, Cross-Origin Resource Sharing）定义了浏览器与服务器如何实现跨源通信。CORS背后的基本思路就是使用自定义的HTTP头部允许浏览器和服务器相互了解，以确实请求或响应应该成功还是失败。  
对于简单的请求，在发送时会有一个额外的头部叫Origin，包含发送请求的页面的源（协议、域名和端口）。
```js
Origin: http://www.nczonline.net
```
如果服务器决定响应请求，那么应该发送Access-Control-Allow-Origin头部，包含相同的源；或者如果资源是公开的，那么就包含"*"。  
```js
Access-Control-Allow-Origin: http://www.nczonline.net
```
现代浏览器通过XMLHttpRequest对象原生支持CORS。在尝试访问不同源的资源时，这个行为会被自动触发。跨域XHR对象也施加了一些额外限制：
- 不能使用setRequestHeader()设置自定义头部。
- 不能发送和接收cookie。
- getAllResponseHeaders()方法始终返回空字符串。
#### 预检请求
CORS通过一种叫预检请求（preflighted request）的服务器验证机制，允许使用自定义头部、复杂请求，以及不同请求体内容类型。在发送复杂请求时，会先向服务器发送一个预检请求，这个请求使用OPTIONS方法发送并包含以下头部：
- Origin：与简单请求相同。
- Access-Control-Request-Method：请求希望使用的方法。
- Access-Control-Request-Headers:（可选）要使用的逗号分隔的自定义头部列表。
在这个请求发送后，服务器可以确定是否允许这种类型的请求。服务器会通过在响应中发送如下头部与浏览器沟通这些信息：
- Access-Control-Allow-Origin：允许浏览器访问的源。
- Access-Control-Allow-Methods：允许的方法（逗号分隔的列表）。
- Access-Control-Allow-Headers：服务器允许的头部（逗号分隔的列表）。
- Access-Control-Max-Age：缓存预检请求的秒数。
预检请求返回后，结果会按响应指定的时间缓存一段时间。换句话说，只有第一次发送这种类型的请求时才会多发送一次额外的HTTP请求。
#### 凭据请求
默认情况下，跨源请求不提供凭据（cookie、HTTP认证和客户端SSL证书）。可以通过将withCredentials属性设置为true来表明请求会发送凭据。如果服务器允许带凭据的请求，那么可以在响应中包含如下HTTP头部：
```
Access-Control-Allow-Credentials: true
```
::: tip 注意
服务器也可以在预检请求的响应中发送这个HTTP头部，以表明这个源允许发送凭据请求。
:::
### 替代性跨源技术
CORS出现之前的一些跨域解决方案，不需要修改服务器。
#### 图片探测
利用`<img>`标签实现跨域通信的最早的一种技术。可以动态创建图片，然后通过它们的onload和onerror事件处理程序得知何时收到响应。  
```js
    let img = new Image();
    img.onload = img.onerror = function() {
      alert("Done! ");
    };
    img.src = "http://www.example.com/test?name=Nicholas";
```
只能发送GET请求、无法获取服务器响应的内容。
#### JSONP
JSON with padding，是在Web服务上流行的一种JSON变体。JSONP格式包含两个部分：回调和数据：
```
http://freegeoip.net/json/?callback=handleResponse
```
JSONP调用是通过动态创建`<script>`元素并为src属性指定跨域URL实现的。
```js
    function handleResponse(response) {
      console.log(`
          You're at IP address ${response.ip}, which is in
          ${response.city}, ${response.region_name}`);
    }
    let script = document.createElement("script");
    script.src = "http://freegeoip.net/json/?callback=handleResponse";
    document.body.insertBefore(script, document.body.firstChild);
```
缺点：不安全，不能确定是否请求成功。
### Fetch API
XMLHttpRequest可以选择异步，而Fetch API则必须是异步。
#### 基本用法
fetch()方法是暴露在全局作用域中的，包括主页面执行线程、模块和工作线程。调用这个方法，浏览器就会向给定URL发送请求。  
```js
let r = fetch('utl')
console.log(r) // Promise
r.then(response => response.text())
.then(text => console.log(text))
```
Fetch API支持通过Response的status（状态码）和statusText（状态文本）属性检查响应状态。  
#### 常见Fetch请求模式
发送JSON数据：
```js
    let payload = JSON.stringify({
      foo: 'bar'
    });
    let jsonHeaders = new Headers({
      'Content-Type': 'application/json'
    });
    fetch('/send-me-json', {
      method: 'POST',    // 发送请求体时必须使用一种HTTP方法
      body: payload,
      headers: jsonHeaders
    });
```
在请求体中发送参数：
```js
    let payload = 'foo=bar&baz=qux';
    let paramHeaders = new Headers({
      'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'
    });
    fetch('/send-me-params', {
      method: 'POST',   // 发送请求体时必须使用一种HTTP方法
      body: payload,
      headers: paramHeaders
    });
```
发送文件：
```js
    let imageFormData = new FormData();
    let imageInput = document.querySelector("input[type='file']");
    imageFormData.append('image', imageInput.files[0]);
    fetch('/img-upload', {
      method: 'POST',
      body: imageFormData
    });
```
发送跨源请求: 需要包含cors头部，或者发送no-cors请求，但是无法得到返回值。  
中断请求：AbortController. abort()会中断所有网络传输。  
#### Headers对象
Headers与Map类型都有get()、set()、has()和delete()等实例方法。  
在初始化Headers对象时，也可以使用键/值对形式的对象，而Map则不可以。  
Headers对象通过append()方法支持添加多个值。  
#### Request对象
```js
    let r = new Request('https://foo.com',init);
    console.log(r);
    // Request {...}
    // 克隆Request对象
    let r2 = r.clone();
    // 使用Request对象，一个对象只能请求一次
    fetch(r);
```
#### Response对象
调用fatch()后，它会返回一个解决为Response对象大的期约：
```js
fetch(url).then((response)=>{
response : {
  body:{}
  status: 200
  statusText: OK
  redirected: false
}
})
```
#### Request、Response及Body混入
没看懂
### Beacon API
关闭页面前发送一个请求，即使原始页面关闭，浏览器也会把这个请求发送出去。  
navigator对象增加了一个sendBeacon()方法。这个简单的方法接收一个URL和一个数据有效载荷参数，并会发送一个POST请求。
### Web Socket
WebSocket的目标是通过一个长时连接实现与服务器全双工、双向的通信。因为Web Socket使用了自定义协议，所以URL方案（scheme）稍有变化：不能再使用http://或https://，而要使用ws://和wss://。  
#### API
创建一个新的Web Socket：
```js
let socket = new WebSocket("ws://www.example.com/server.php");
    socket.close(); // 关闭
```
同源策略不适用于webscoket，可以连接任何站点。  
WebSocket有一个readyState属性表示当前状态：
- WebSocket.OPENING（0）：连接正在建立。
- WebSocket.OPEN（1）：连接已经建立。
- WebSocket.CLOSING（2）：连接正在关闭。
- WebSocket.CLOSE（3）：连接已经关闭。
#### 发送和接收数据
要向服务器发送数据，使用send()方法并传入一个字符串、ArrayBuffer或Blob。 
服务器向客户端发送消息时，WebSocket对象上会触发message事件。   
```js
    socket.onmessage = function(event) {
      let data = event.data;
      // 对数据执行某些操作
    };
```
#### 其他事件
- open：在连接成功建立时触发。
- error：在发生错误时触发。连接无法存续。
- close：在连接关闭时触发。
### 安全
在未授权系统可以访问某个资源时，可以将其视为跨站点请求伪造(CSRF)攻击。  
需要验证请求发送者拥有对资源的访问权限。可以通过如下方式实现：
- 要求通过SSL访问能够被Ajax访问的资源。
- 要求每个请求都发送一个按约定算法计算好的令牌（token）。
- 要求POST而非GET请求（很容易修改请求方法）。
- 使用来源URL验证来源（来源URL很容易伪造）。
- 基于cookie验证（同样很容易伪造）。

## 二十五、客户端存储
### cookie
cookie在浏览器中是由以下参数构成的：
- 名称name：唯一标识cookie的名称。不区分大小写
- 值value：存储在cookie里的字符串值。这个值必须经过URL编码。
- 域domain：cookie有效的域。发送到这个域的所有请求都会包含对应的cookie。
- 路径path：请求URL中包含这个路径才会把cookie发送到服务器。
- 过期时间expires：表示何时删除cookie的时间戳。
- 安全标志secure：设置之后，只在使用SSL安全连接的情况下才会把cookie发送到服务器。
域、路径、过期时间和secure标志用于告诉浏览器什么情况下应该在请求中包含cookie。这些参数并不会随请求发送给服务器，实际发送的只有cookie的名/值对。  
#### JavaScript中的cookie
document.cookie = "name=xxx"就可以设置，最好还是使用encodeURIComponent()对名称和值进行编码：
```js
    document.cookie = encodeURIComponent("name") + "=" +
                      encodeURIComponent("Nicholas");
```
#### 子cookie
为绕过浏览器对每个域cookie数的限制,在单个cookie存储的小块数据:
```js
    name=name1=value1&name2=value2&name3=value3&name4=value4&name5=value5
```
#### 使用cookie的注意事项
HTTP-only的cookie，只能在服务器读取，可以在浏览器设置。  

### Web Storage
WebStorage的目的是解决通过客户端存储不需要频繁发送回服务器的数据时使用cookie的问题。  
localStorage是永久存储机制，sessionStorage是跨会话的存储机制。  
#### Storage类型
Storage类型用于保存名/值对数据，有以下方法：
- clear()：删除所有值；不在Firefox中实现。
- getItem（name）：取得给定name的值。
- key（index）：取得给定数值位置的名称。
- removeItem（name）：删除给定name的名/值对。
- setItem（name, value）：设置给定name的值。
 Storage类型只能存储字符串。非字符串数据在存储之前会自动转换为字符串。  
#### sessionStorage对象
sessionStorage对象只存储会话数据，这意味着数据只会存储到浏览器关闭。  
#### localStorage对象
要访问同一个localStorage对象，页面必须来自同一个域（子域不可以）、在相同的端口上使用相同的协议。  
存储在localStorage中的数据会保留到通过JavaScript删除或者用户清除浏览器缓存。  
#### 存储事件
每当Storage对象发生变化时，都会在文档上触发storage事件。
#### 限制

### IndexedDB
Indexed Database API简称IndexedDB，是浏览器中存储结构化数据的一个方案。  
#### 数据库
IndexedDB使用对象存储而不是表格保存数据。
```js
    let db,
        request,
        version = 1;
    request = indexedDB.open("admin", version); // 有则返回，无则创建
    request.onerror = (event) =>
      alert(`Failed to open: ${event.target.errorCode}`);
    request.onsuccess = (event) => {
      db = event.target.result; // 数据库实例
    };
```
#### 对象存储
```js

    request.onupgradeneeded = (event) => {
      const db = event.target.result;
      // 如果存在则删除当前objectStore。测试的时候可以这样做
      // 但这样会在每次执行事件处理程序时删除已有数据
      if (db.objectStoreNames.contains("users")) {
        db.deleteObjectStore("users");
      }
      db.createObjectStore("users", { keyPath: "username" });
    };
```
#### 事务
```js
    let transaction = db.transaction("users");// 不传参数对所有数据库有读取权限，传参对对应数据库有读权限 也可以传字符串数组，访问多个数据库
```
第二个参数决定权限："readonly"、"readwrite"或"versionchange"。  
```js
    const transaction = db.transaction("users"),
        store = transaction.objectStore("users"),
        request = store.get("007");
        store.add()
        store.put()
        store.delete()
        store.clear()
    request.onerror = (event) => alert("Did not get the object! ");
    request.onsuccess = (event) => alert(event.target.result.firstName);
```
#### 插入对象
add()和put()都接收新对象插入数据库，遇到同名数据时，add会报错，put会更新对象。  
#### 通过游标查询
暂时跳过。

## 二十六、模块
### 理解模块模式
把逻辑分块，各自封装，相互独立，每个块自行决定对外暴露什么，同时自行决定引入执行哪些外部代码。  
#### 模块标识符
模块系统本质上是键/值实体，其中每个模块都有个可用于引用它的标识符。这个标识符在模拟模块的系统中可能是字符串，在原生实现的模块系统中可能是模块文件的实际路径。
#### 模块依赖
本地模块向模块系统声明一组外部模块（依赖），这些外部模块对于当前模块正常运行是必需的。模块系统检视这些依赖，进而保证这些外部模块能够被加载并在本地模块运行时初始化所有依赖。  
#### 模块加载
只有整个依赖图都加载完成，才可以执行入口模块。
#### 入口
相互依赖的模块必须指定一个模块作为入口（entry point），这也是代码执行的起点。
#### 异步依赖
让JavaScript通知模块系统在必要时加载新模块，并在模块加载完成后提供回调。
#### 动态依赖

#### 静态分析
分析工具会检查代码结构并在不实际执行代码的情况下推断其行为。对静态分析友好的模块系统可以让模块打包系统更容易将代码处理为较少的文件。
#### 循环依赖
A->B->C->A 

### 凑合的模块系统
ES6之前的模块有时候会使用函数作用域和立即调用函数表达式（IIFE, ImmediatelyInvoked Function Expression）将模块定义封装在匿名闭包中。模块定义是立即执行的。

### 使用ES6之前的模块加载器
#### CommonJS
CommonJS模块语法不能在浏览器中直接运行。   
CommonJS模块定义需要使用require()指定依赖，而使用exports对象定义自己的公共API：
```js
    var moduleB = require('./moduleB');
    module.exports = {
      stuff: moduleB.doStuff();
    };
```
无论一个模块在require()中被引用多少次，模块永远是单例。  
模块第一次加载后会被缓存，后续加载会取得缓存的模块。  
在CommonJS中，模块加载是模块系统执行的同步操作。（运行到对应代码时加载）  
```js 
    console.log('moduleA');
    if (loadCondition) {
      require('./moduleA');
    }
```
模块不会指定自己的标识符，它们的标识符由其在模块文件层级中的位置决定。  
module.exports:
```js
    module.exports = 'foo';
        
    module.exports = {
      a: 'A',
      b: 'B'
    };
    // 等价操作：
    module.exports.a = 'A';
    module.exports.b = 'B';

    // 作为类导出
    class A {}
    module.exports = A;
    var A = require('./moduleA');
    var a = new A();

    // 作为实例导出
    class A {}
    module.exports = new A();
```
#### 异步模块定义
异步模块定义（AMD, AsynchronousModule Definition）的模块定义系统则以浏览器为目标执行环境，这需要考虑网络延迟的问题。AMD的一般策略是让模块声明自己的依赖，而运行在浏览器中的模块系统会按需获取依赖，并在依赖加载完成后立即执行依赖它们的模块。 
AMD加载器会在所有依赖模块加载完毕后立即调用模块工厂函数。   
AMD支持可选地为模块指定字符串标识符。  
```js
    // ID为’moduleA’的模块定义。moduleA依赖moduleB，
    // moduleB会异步加载
    define('moduleA', ['moduleB'], function(moduleB) {
      return {
        stuff: moduleB.doStuff();
      };
    });
```
#### 通用模块定义
为了统一CommonJS和AMD生态系统，通用模块定义（UMD）规范应运而生。UMD可用于创建这两个系统都可以使用的模块代码。本质上，UMD定义的模块会在启动时检测要使用哪个模块系统，然后进行适当配置，并把所有逻辑包装在一个立即调用的函数表达式（IIFE）中。
### 使用ES6模块
#### 模块标签及定义
带有type="module"属性的`<script>`标签会告诉浏览器相关代码应该作为模块执行，而不是作为传统的脚本执行。模块可以嵌入在网页中，也可以作为外部文件引入：
```html
    <script type="module">
      // 模块代码
    </script>
    <script type="module" src="path/to/myModule.js"></script>
```
所有模块都会像`<script defer>`加载的脚本一样按顺序执行。(立即下载模块文件，但执行会延迟到文档解析完成。)  `<script type="module">`在页面中出现的顺序就是它们执行的顺序。  
```html
    <!-- 第二个执行-->
    <script type="module"></script>
    <!-- 第三个执行-->
    <script type="module"></script>
    <!-- 第一个执行-->
    <script></script>
```
#### 模块加载
ESModule既可以通过浏览器原生加载，也可以与第三方加载器和构建工具一起加载。ES6模块加载是异步的，这个异步递归加载过程会持续到整个应用程序的依赖图都解析完成。解析完依赖图，应用程序就可以正式加载模块了。
#### 模块行为
CommonJS共有特性：
- 模块代码只在加载后执行。
- 模块只能加载一次。
- 模块是单例。
- 模块可以定义公共接口，其他模块可以基于这个公共接口观察和交互。
- 模块可以请求加载其他模块。
- 支持循环依赖。
ES6独有特性：
- ES6模块默认在严格模式下执行。
- ES6模块不共享全局命名空间。
- 模块顶级this的值是undefined（常规脚本中是window）。
- 模块中的var声明不会添加到window对象。
- ES6模块是异步加载和执行的。

#### 模块导出
ES6模块支持两种导出：命名导出和默认导出。通过export关键字导出。不允许嵌套。  
命名导出（named export）就好像模块是被导出值的容器：
```js
export const foo = 'foo'

let foo = 'foo'
export foo

export { foo }

export { foo as bar } //指定别名

```
默认导出（default export）就好像模块与被导出的值是一回事，这个模块本身就是导出的值。
```js
    const foo = 'foo';
    export default foo

    // 等同于export default foo;
    export { foo as default };

    export foo
```
因为命名导出和默认导出不会冲突，所以ES6支持在一个模块中同时定义这两种导出。 

```js
    // 命名行内导出
    export const baz = 'baz';
    export const foo = 'foo', bar = 'bar';
    export function foo() {}
    export function＊ foo() {}
    export class Foo {}
    // 命名子句导出
    export { foo };
    export { foo, bar };
    export { foo as myFoo, bar };
    // 默认导出
    export default 'foo';
    export default 123;
    export default /[a-z]＊/;
    export default { foo: 'foo' };
    export { foo, bar as default };
    export default foo
    export default function() {}
    export default function foo() {}
    export default function＊() {}
    export default class {}
    // 会导致错误的不同形式：
    // 行内默认导出中不能出现变量声明
    export default const foo = 'bar';
    // 只有标识符可以出现在export子句中
    export { 123 as foo }
    // 别名只能在export子句中出现
    export const foo = 'foo' as myFoo;
```

#### 模块导入
import必须出现在模块的顶级，import语句被提升到模块顶部。
导入对模块而言是只读的，实际上相当于const声明的变量。在使用*执行批量导入时，赋值给别名的命名导出就好像使用Object.freeze()冻结过一样。  
命名导出和默认导出的区别也反映在它们的导入上。命名导出可以使用＊批量获取并赋值给保存导出集合的别名，而无须列出每个标识符：
```js
    // module.js
    const foo = 'foo', bar = 'bar', baz = 'baz';
    export { foo, bar, baz }
    export default foo
    // index.js
    import * as Foo from './foo.js';
    import { foo, bar, baz } from './foo.js';
    import foo from './foo.js';
    console.log(Foo.foo); // foo
    console.log(Foo.bar); // bar
    console.log(Foo.baz); // baz

```
#### 模块转移导出
模块导入的值可以直接通过管道转移到导出。
```js
export * from './foo.js';
export { foo, bar as myBar } from './foo.js';
export { default } from './foo.js';
export { foo as default } from './foo.js';
```
#### 工作者模块
CMAScript 6模块与Worker实例完全兼容。Worker构造函数接收第二个参数，用于说明传入的是模块文件。  
```js
    // 第二个参数默认为{ type: 'classic' }
    const scriptWorker = new Worker('scriptWorker.js');
    const moduleWorker = new Worker('moduleWorker.js', { type: 'module' });
```
#### 向后兼容
```js
    // 支持模块的浏览器会执行这段脚本
    // 不支持模块的浏览器不会执行这段脚本
    <script type="module" src="module.js"></script>
    // 支持模块的浏览器不会执行这段脚本
    // 不支持模块的浏览器会执行这段脚本
    <script nomodule src="script.js"></script>
```

## 二十七、工作者线程
### 工作者线程简介
使用工作者线程，浏览器可以在原始页面环境之外再分配一个完全独立的二级子环境。这个子环境不能与依赖单线程交互的API（如DOM）互操作，但可以与父环境并行执行代码。
#### 工作者线程与线程
工作者线程是以实际线程实现的。工作者线程能够使用SharedArrayBuffer在多个环境间共享内容。工作者线程相对比较重，不建议大量使用。
#### 工作者线程的类型
专用工作者线程、共享工作者线程和服务工作者线程。  
专用工作者线程，通常简称为工作者线程、Web Worker或Worker，可以让脚本单独创建一个JavaScript线程，只能被创建它的页面使用。  
共享工作者线程可以被多个不同的上下文使用，包括不同的页面。  
服务工作者线程的主要用途是拦截、重定向和修改页面发出的请求，充当网络请求的仲裁者的角色。  
####  WorkerGlobalScope
在工作者线程内部，没有window的概念。这里的全局对象是WorkerGlobalScope的实例，通过self关键字暴露出来。  
self上可用的属性是window对象上属性的严格子集。其中有些属性会返回特定于工作者线程的版本。
### 专用工作者线程
专用工作者线程可以与父页面交换信息、发送网络请求、执行文件输入/输出、进行密集计算、处理大量数据，以及实现其他不适合在页面执行线程里做的任务。
#### 专用工作者线程的基本概念
可以把专用工作者线程称为后台脚本（background script）。  
工作者线程的脚本文件只能从与父页面相同的源加载。  
Worker()构造函数返回的Worker对象是与刚创建的专用工作者线程通信的连接点。  
Worker对象支持下列事件与属性：addEventListener('xx', handler)也可以接收时间
- onerror：在工作者线程中发生ErrorEvent类型的错误事件时 （）
- onmessage：在工作者线程中发生MessageEvent类型的消息事件时
- onmessageerror：在工作者线程中发生MessageEvent类型的错误事件时
- postMessage()：用于通过异步消息事件向工作者线程发送信息。
- terminate()：用于立即终止工作者线程。
在专用工作者线程内部，全局作用域是DedicatedWorkerGlobalScope的实例，通过self关键字访问该全局作用域。  
DedicatedWorkerGlobalScope在WorkerGlobalScope基础上增加了以下属性和方法：
- name：可以提供给Worker构造函数的一个可选的字符串标识符。
- postMessage()：与worker.postMessage()对应的方法，用于从工作者线程内部向父上下文发送消息。
- close()：与worker.terminate()对应的方法，用于立即终止工作者线程。
- importScripts()：用于向工作者线程中导入任意数量的脚本。

#### 专用工作者线程的生命周期
三个状态：初始化（initializing）、活动（active）和终止（terminated）  
可以再初始化时通过postMessage()发送消息，工作者线程初始化完毕后会自动执行。  
一旦调用了terminate()，工作者线程的消息队列就会被清理并锁住，close()会通知工作者线程取消事件循环中的所有任务，并阻止继续添加新任务。  
#### 配置Worker选项
Worker构造函数的第二个参数是一个对象，用于配置工作者线程：
- name：可以在工作者线程中通过self.name读取到的字符串标识符。
- type：表示加载脚本的运行方式，可以是"classic"或"module"。"classic"将脚本作为常规脚本来执行，"module"将脚本作为模块来执行。
- credentials：在type为"module"时，指定如何获取与传输凭证数据相关的工作者线程模块脚本。值可以是"omit"、"same-orign"或"include"。这些选项与fetch()的凭证选项相同。在type为"classic"时，默认为"omit"。

#### 在JavaScript行内创建工作者线程
工作者线程需要基于脚本文件来创建，但这并不意味着该脚本必须是远程资源。专用工作者线程也可以通过Blob对象URL在行内脚本创建。  
```js
const blod = new Blob([`self.onmessage = console.log`])
const worker = new Worker(URL.createObjectURL(blod))
worker.postMessage('hello')
```
可以利用函数序列化(toString)初始化工作者线程脚本：
```js
function consoseLog(msg) {
  console.log(msg.data)
}
const blod = new Blob([`self.onmessage = ${consoseLog.toString()}`])
const worker = new Worker(URL.createObjectURL(blod))
worker.postMessage('hello')
```
#### 在工作者线程中动态执行脚本
工作者线程中的脚本可以使用importScripts()方法通过编程方式加载和执行任意脚本。  
importScripts()方法可以接收任意数量的脚本作为参数。浏览器下载它们的顺序没有限制，但执行则会严格按照它们在参数列表的顺序进行：
```js
    // main.js
    const worker = new Worker('./worker.js');
    // scriptA.js
    console.log('scriptA executes');
    // scriptB.js
    console.log('scriptB executes');
    // worker.js
    console.log('importing scripts');
    importScripts('./scriptA.js')
    importScripts('./scriptB.js')
    // 等价于
    importScripts('./scriptA.js', './scriptB.js')
```
#### 委托任务到子工作者线程
在工作者线程中再创建子工作者线程。子工作者线程的脚本路径根据父工作者线程而不是相对于网页来解析。  
#### 处理工作者线程错误
try/catch无法捕捉工作者线程的错误，，需要在Worker对象上添加onerror事件。  
#### 与专用工作者线程通信
1. 使用postMessage()
2. 使用MessageChannel
3. 使用BroadcastChannel

#### 工作者线程数据传输
工作者线程是独立的上下文，因此在上下文之间传输数据就会产生消耗。在JavaScript中，有三种在上下文间转移信息的方式：结构化克隆算法（structured clone algorithm）、可转移对象（transferable objects）和共享数组缓冲区（shared arraybuffers）。  
- 结构化克隆算法可用于在两个独立上下文间共享数据。在通过postMessage()传递对象时，浏览器会遍历该对象，并在目标上下文中生成它的一个副本。消耗比较大。
- 可转移对象可以把所有权从一个上下文转移到另一个上下文，只支持ArrayBuffer、MessagePort、 ImageBitmap、 OffscreenCanvas。
```js
    // 结构化克隆
    const worker = new Worker('./worker.js');
    const arrayBuffer = new ArrayBuffer(32);
    worker.postMessage(arrayBuffer);
    // 可转移对象
    worker.postMessage(arrayBuffer, [arrayBuffer]);
```
- SharedArrayBuffer 在把SharedArrayBuffer传给postMessage()时，浏览器只会传递原始缓冲区的引用。结果是，两个不同的JavaScript上下文会分别维护对同一个内存块的引用。容易发生资源征用。  可使用Atomics对象让一个工作者线程获得SharedArrayBuffer实例的锁。

#### 线程池
因为启用工作者线程代价很大，所以某些情况下可以考虑始终保持固定数量的线程活动，需要时就把任务分派给它们。  
线程数量可参考navigator.hardwareConcurrency属性返回的系统可用的核心数量。 

### 共享工作者线程
共享工作者线程或共享线程与专用工作者线程类似，但可以被多个可信任的执行上下文访问。  
#### 共享工作者线程简介
```js
    const sharedWorker = new SharedWorker('./worker.js');
```
SharedWorker()则只会在相同的标识不存在的情况下才创建新实例。如果的确存在与标识匹配的共享工作者线程，则只会与已有共享者线程建立新的连接。不同的线程名称会强制浏览器创建多个共享工作者线程：
```js
    // 实例化一个共享工作者线程
    //   - 全部基于同源调用构造函数
    //   - 所有脚本解析为相同的URL
    //   - 一个线程名称为’foo'，一个线程名称为’bar'
    new SharedWorker('./sharedWorker.js', {name: 'foo'});
    new SharedWorker('./sharedWorker.js', {name: 'foo'});
    new SharedWorker('./sharedWorker.js', {name: 'bar'});
```
没有办法以编程方式终止共享线程，共享线程实例上没有terminate()方法。

#### 连接到共享工作者线程
每次调用SharedWorker()构造函数，无论是否创建了工作者线程，都会在共享线程内部触发connect事件。  

### 服务工作者线程
服务工作者线程（service worker）是一种类似浏览器中代理服务器的线程，可以拦截外出请求和缓存响应。  
来自一个域的多个页面共享一个服务工作者线程。  
服务工作者线程在两个主要任务上最有用：充当网络请求的缓存层和启用推送通知。  
强制刷新会强制浏览器忽略所有网络缓存，而服务工作者线程对大多数主流浏览器而言就是网络缓存。  
#### 服务工作者线程基础
服务工作者线程没有全局构造函数，通过ServiceWorkerContainer管理：
```js
    navigator.serviceWorker.register('./serviceWorker.js');
```

## 二十八、最佳实践
### 可维护性
#### 什么是可维护的代码
- 容易理解：无须求助原始开发者，任何人一看代码就知道它是干什么的，以及它是怎么实现的。
- 符合常识：代码中的一切都显得顺理成章，无论操作有多么复杂。
- 容易适配：即使数据发生变化也不用完全重写。
- 容易扩展：代码架构经过认真设计，支持未来扩展核心功能。
- 容易调试：出问题时，代码可以给出明确的信息，通过它能直接定位问题。

#### 编码规范
1. 可读性
以下地方应该写注释：函数和方法、大型代码块、复杂的算法、使用黑科技
2. 变量和函数命名
- 变量名应该是名词，例如car或person。
- 函数名应该以动词开始，例如getName()。返回布尔值的函数通常以is开头，比如isEnabled()。
- 变量、函数和方法应该以小写字母开头，使用驼峰大小写（camelCase）形式，如getName()和isPerson。类名应该首字母大写，如Person、RequestFactory。常量值应该全部大写并以下划线相接，比如REQUEST_TIMEOUT。
3. 变量类型透明化

#### 松散耦合

#### 编码惯例
如果你不负责创建维护某个对象则：
- 不要给实例或原型添加属性。
- 不要给实例或原型添加方法。
- 不要重定义已有的方法。
需要修改就继承别人的对象，自己想怎么改就怎么改。  
不要比较null，使用类型比较。  
- 如果值应该是引用类型，则使用instanceof操作符检查其构造函数。
- 如果值应该是原始类型，则使用typeof检查其类型。
- 如果希望值是有特定方法名的对象，则使用typeof操作符确保对象上存在给定名字的方法。
使用常量。  

### 性能
JavaScript一开始就是一门解释型语言，因此执行速度比编译型语言要慢一些。Chrome是第一个引入优化引擎将JavaScript编译为原生代码的浏览器。
#### 作用域意识
1. 避免全局查找
2. 不使用with语句
3. 避免不必要的属性查找
常量和变量里面的值，数组元素都是O(1)复杂度，访问非常快。  
访问对象属性的算法复杂度是O（n）。  
避免通过多次查找获取一个值，使用对象的object属性超过一次，就应将其保存在局部变量中。  
如果实现某个需求既可以使用数组的数值索引，又可以使用命名属性，那就都应该使用数值索引。 
4. 优化循环
简化终止条件、简化循环体、使用后测试循环(do while)
```js
for(let i=0;i<values.length;i++)
// 改成这样更快
for(let i=values.length;i>=0;i--)
// 因为访问values.length的复杂度是O(n)，访问0的复杂度是O(1)
```
5. 展开循环
如果循环次数固定，可以抛弃循环，直接多次调用。  
如果循环体过大，可以用**达夫设备**，每8次为一个循环。  
6. 避免重复解释
应尽量避免把js代码当作字符串传递。
7. 其他性能优化注意事项
- 原生方法很快，Math是使用C++写的
- switch语句很快，复杂if-else应该用switch，把最可能的放前面
- 位操作很快

#### 语句最少化
avaScript代码中语句的数量影响操作执行的速度。一条可以执行多个操作的语句，比多条语句中每个语句执行一个操作要快。  
1. 多个变量声明使用一个语句。
2. 插入迭代性值
```js
    let name = values[i];
    i++;
    // 这样更快
    let name = values[i++];
```
3. 使用数组和对象字面量
```js
let a = [1,2,3] // 比 new Array快
let a = {
  name:1
}
// 比let a = new Object快
```
#### 优化DOM交互
JavaScript代码中，涉及DOM的部分无疑是非常慢的。
1. 实时更新最小化
实时更新的次数越多，执行代码所需的时间也越长。反之，实时更新的次数越少，代码执行就越快。  
使用文档片段构建DOM结构，然后一次性将它添加到list元素。  
2. 使用innerHTML
大量DOM更新，innerHTML比appendChild()要快
3. 使用事件委托
事件委托利用了事件的冒泡。
4. 注意HTMLCollection
只要返回HTMLCollection对象，就应该尽量不访问它。

### 部署
#### 构建流程
摇树优化（tree shaking），确定代码中哪些部分是不需要的。最终打包得到的文件可以瘦身很多。
模块打包器的工作是识别应用程序中涉及的JavaScript依赖关系，将它们组合成一个大文件。

#### 验证
JSLint和ESLint

#### 压缩
代码大小（code size）和传输负载（wire weight）。
1. 代码压缩
2. JavaScript编译
3. JavaScript转译
转译可以将现代的代码转换成更早的ECMAScript版本，
4. HTTP压缩

## 附录A ES2018和ES2019
ECMAScript 2018于2018年1月完成，主要增加了异步迭代、剩余和扩展操作符、正则表达式和期约等方面的特性。
### 数组打平方法
ECMAScript 2019在Array.prototype上增加了两个方法：flat()和flatMap()。这两个方法为打平数组提供了便利。如果没有这两个方法，则打平数组就要使用迭代或递归。
#### Array.prototype.flat()
```js
    // 如果没有这两个方法
    function flatten(sourceArray, flattenedArray = []) {
      for (const element of sourceArray) {
        if (Array.isArray(element)) {
          flatten(element, flattenedArray);
        } else {
          flattenedArray.push(element);
        }
      }
      return flattenedArray;
    }
    const arr = [[0], 1, 2, [3, [4, 5]], 6];
    console.log(flatten(arr))
    // [0, 1, 2, 3, 4, 5, 6]
    arr.flat() // [0, 1, 2, 3, [4, 5], 6];
    arr.flat(2)  // [0, 1, 2, 3, 4, 5, 6]
```
depth参数（默认值为1），表示要打平到几级，返回一个浅复制的数组。  

#### Array.prototype.flatMap()
Array.prototype.flatMap()方法会在打平数组之前执行一次映射操作。在功能上，arr.flatMap(f)与arr.map(f).flat()等价；

### Object.fromEntries()
ECMAScript 2019又给Object类添加了一个静态方法fromEntries()，用于通过键/值对数组的集合构建对象。
```js
    const map = new Map().set('foo', 'bar');
    console.log(Object.fromEntries(map));
    //{foo:'bar'}
```
### 字符串修理

ECMAScript 2019向String.prototype添加了两个新方法：trimStart()和trimEnd()。它们分别用于删除字符串开头和末尾的空格。

###  Symbol.prototype.description
ECMAScript 2019在Symbol.prototype上增加了description属性，用于取得可选的符号描述。
```js
    const s = Symbol('foo');
    console.log(s.toString());
    // Symbol(foo)
s..description// foo
```
### 可选的catch绑定
ECMAScript 2019 catch(e) 中的(e)可以省略

## 附录B 严格模式
ECMAScript 5首次引入严格模式的概念。严格模式用于选择以更严格的条件检查JavaScript代码错误，可以应用到全局，也可以应用到函数内部。
### 选择使用
use strict
### 变量
```js
    // 变量未声明
    // 非严格模式：创建全局变量
    // 严格模式：抛出ReferenceError
    message = "Hello world! ";
    // 删除变量
    // 非严格模式：静默失败
    // 严格模式：抛出ReferenceError
    let color = "red";
    delete color;
```
不允许变量名为implements、interface、let、package、private、protected、public、static和yield。 
### 对象
- 给只读属性赋值会抛出TypeError。
- 在不可配置属性上使用delete会抛出TypeError。
- 给不存在的对象添加属性会抛出TypeError。

### 函数
```js
    // 命名参数重名
    // 非严格模式：没有错误，只有第二个参数有效
    // 严格模式：抛出SyntaxError
    function sum (num, num){
      // 函数代码
    }
```
在严格模式下，命名参数和arguments是相互独立的。去掉了arguments.callee和arguments.caller。
```js
    // 在if语句中声明函数
    // 非严格模式：函数提升至if语句外部
    // 严格模式：抛出SyntaxError
    if (true){
      function doSomething(){
        // ...
      }
    }
```
严格模式明确不允许使用eval和arguments作为标识符和操作它们的值。 
### this强制转型
在严格模式下，则始终以指定值作为函数this的值，无论指定的是什么值。非严格模式，null或undefined会被转型为window。
### 类与模块
ES6类和模块中定义的所有代码默认都处于严格模式。
### 其他变化
- 消除with语句
- 去掉了八进制字面量

## 附录C JavaScript库和框架
### 框架
“框架”（framework）涵盖各种不同的模式，但各自具有不同的组织形式，用于搭建复杂应用程序。JavaScript框架越来越多地表现为单页应用程序（SPA, Single PageApplication）。SPA使用HTML5浏览器历史API，在只加载一个页面的情况下通过URL路由提供完整的应用程序用户界面。
### 通用库
所有通用库都致力于通过将常用功能封装为新API，来补偿浏览器接口、弥补实现差异。  
Lodash提供了很多操作原生类型，如数组、对象、函数和原始值的增强方法。  

### 动画与特效
D3 three.js

## 附录D JavaScript工具
### 包管理
npm，即Node包管理器（Node Package Manager）
### 模块加载器
require.js，即Require.js，一个基于AMD的模块加载器。
### 模块打包器
模块打包器可以将任意格式、任意数量的模块合并为一个或多个文件，供客户端加载。
Webpack、 JSPM、Browserify、Rollup
### 编译/转译工具及静态类型系统
Babel、TypeScript
### 高性能脚本工具
WebAssembly、asm.js
### 构建工具、自动化系统和任务运行器
Grunt、Gulp
### 代码检查和格式化
ESLint、JSLint
### 压缩工具
Uglify、Google Closure Compiler
### 单元测试
测试驱动开发（TDD, TestDriven Development）是以单元测试为中心的软件开发过程。
Mocha、Jasmine、JsUnit
### 文档生成器