## 1.跨域的实现方法

#### CORS(Cross-Origin Resource Sharing，跨源资源共享)

使用自定义的HTTP 头部让浏览器与服务器进行沟通，从而决定请求或响应是应该成功，还是应该失败。

#### JSONP

通过script标签引入一个js文件，这个js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入。所以jsonp是需要服务器端的页面进行相应的配合的。

#### document.domain

对于主域相同而子域不同的例子，可以通过设置document.domain的办法来解决。
具体的做法是可以在http://www.a.com/a.html 和http://script.a.com/b.html 两个文件中分别设置`document.domain = 'a.com'`，然后通过a.html文件中创建一个iframe，去控制iframe的contentDocument，这样两个js文件之间就可以“交互”了。

#### window.postMessage

允许两个窗口/帧之间跨域发送数据消息。从本质上讲，window.postMessage是一个跨域的无服务器垫片的Ajax。

#### window.name

window对象有个`name`属性，该属性有个特征：即在一个窗口(window)的生命周期内,窗口载入的所有的页面都是共享一个window.name的，每个页面对window.name都有读写的权限，window.name是持久存在一个窗口载入过的所有页面中的，并不会因新页面的载入而进行重置。

### 详情请参考:

http://www.cnblogs.com/2050/p/3191744.html

http://www.cnblogs.com/yzg1/p/5070037.html

http://blog.csdn.net/joyhen/article/details/21631833

https://mp.weixin.qq.com/s/NOmsbKZsryTUONQj2gBFIA

## 2.jsonp的实现原理

#### 页面上 script 标签可以跨域，并且其 src 指定的js脚本到达浏览器会执行的特性，利用script标签的这一特性，将数据使用json格式用一个函数包裹起来，然后在进行访问的页面中定义一个相同函数名的函数，因为 script 标签src引用的js脚本到达浏览器时会执行，而我们有定义了一个同名的函数，所以json格式的数据，就做完参数传递给了我们定义的同名函数了。这样就完成了跨域数据交换。

### 详情请参考:

http://www.cnblogs.com/digdeep/p/4170059.html

## 3.jsonp优缺点

####   1.优点

1. 它不像XMLHttpRequest对象实现的Ajax请求那样受到同源策略的限制，JSONP可以跨越同源策略；
2. 它的兼容性更好，在更加古老的浏览器中都可以运行，不需要XMLHttpRequest或ActiveX的支持
3. 在请求完毕后可以通过调用callback的方式回传结果。将回调方法的权限给了调用方。这个就相当于将controller层和view层终于分开了。我提供的jsonp服务只提供纯服务的数据，至于提供服务以 后的页面渲染和后续view操作都由调用者来自己定义就好了。如果有两个页面需要渲染同一份数据，你们只需要有不同的渲染逻辑就可以了，逻辑都可以使用同 一个jsonp服务。

####  **2.缺点**

1. 它只支持GET请求而不支持POST等其它类型的HTTP请求
2. 它只支持跨域HTTP请求这种情况，不能解决不同域的两个页面之间如何进行JavaScript调用的问题。
3. jsonp在调用失败的时候不会返回各种HTTP状态码。
4. 缺点是安全性。万一假如提供jsonp的服务存在页面注入漏洞，即它返回的javascript的内容被人控制的。那么结果是什么？所有调用这个 jsonp的网站都会存在漏洞。于是无法把危险控制在一个域名下…所以在使用jsonp的时候必须要保证使用的jsonp服务必须是安全可信的。

## 4.ES6简介，箭头函数与function区别，promise的特点

### let, const

- 这两个的用途与`var`类似，都是用来声明变量的，但在实际运用中他俩都有各自的特殊用途。
- `let`则实际上为JavaScript新增了块级作用域。用它所声明的变量，只在`let`命令所在的代码块内有效，不允许在相同作用域内，重复声明同一个变量。
- `const`也用来声明变量，但是声明的是常量。一旦声明，常量的值就不能改变。
- `const`实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指针，`const`只能保证这个指针是固定的，至于它指向的数据结构是不是可变的，就完全不能控制了。因此，将一个对象声明为常量必须非常小心。

#### 字符串的扩展

- 字符串的遍历器接口`for...of`循环遍历

  ```javascript
  for (let codePoint of 'foo') {
    console.log(codePoint)
  }
  ```

- **includes()**：返回布尔值，表示是否找到了参数字符串。

- **startsWith()**：返回布尔值，表示参数字符串是否在原字符串的头部。

- **endsWith()**：返回布尔值，表示参数字符串是否在原字符串的尾部。

- `repeat`方法返回一个新字符串，表示将原字符串重复`n`次。

- 模板字符串 

- ..................................................................等

#### 数组的扩展

- includes() 方法返回一个布尔值，表示某个数组是否包含给定的值
- `keys()`是对键名的遍历、`values()`是对键值的遍历，`entries()`是对键值对的遍历。
- `fill`方法使用给定值，填充一个数组。
- `find`方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为`true`的成员，然后返回该成员。如果没有符合条件的成员，则返回`undefined`。`findIndex`方法的用法与`find`方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回`-1`。
- `copyWithin`方法，在当前数组内部，将指定位置的成员复制到其他位置（会覆盖原有成员），然后返回当前数组。也就是说，使用这个方法，会修改当前数组。
- `Array.of`方法用于将一组值，转换为数组。
- `Array.from`方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。
- 扩展运算符（spread）是三个点（`...`）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。
- ..................................................................等

#### 函数的扩展

- 函数参数的默认值，直接写在参数定义的后面
- 函数的`length`属性，将返回没有指定默认值的参数个数。也就是说，指定了默认值后，`length`属性将失真。
- 参数的默认值，函数进行声明初始化时，参数会形成一个单独的作用域（context）。等到初始化结束，这个作用域就会消失。这种语法行为，在不设置参数默认值时，是不会出现的。
- rest 参数（形式为`...变量名`），用于获取函数的多余参数，这样就不需要使用`arguments`对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。
- 箭头函数
  - 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。
  - 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。
  - 不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
  - 不可以使用`yield`命令，因此箭头函数不能用作 Generator 函数。

#### 变量的解构赋值

从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

#### Symbol

- 通过`Symbol`函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。
- `Symbol`函数前不能使用`new`命令，否则会报错。这是因为生成的 Symbol 是一个原始类型的值，不是对象。也就是说，由于 Symbol 值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。
- `Symbol`函数可以接受一个字符串作为参数，表示对 Symbol 实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分。

#### Set 和 Map 数据结构

- set类似于数组，但是成员的值都是唯一的，没有重复的值。Set 本身是一个构造函数，用来生成 Set 数据结构。
- Map 类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

## Promise

- Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了`Promise`对象。

- 简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

- `Promise`对象有以下两个特点。

  （1）对象的状态不受外界影响。`Promise`对象代表一个异步操作，有三种状态：`Pending`（进行中）、`Fulfilled`（已成功）和`Rejected`（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是`Promise`这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。

  （2）一旦状态改变，就不会再变，任何时候都可以得到这个结果。`Promise`对象的状态改变，只有两种可能：从`Pending`变为`Fulfiled`和从`Pending`变为`Rejected`。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 Resolved（已定型）。如果改变已经发生了，你再对`Promise`对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

## class

`class`可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的`class`写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

#### module

 模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。

### 详情请参考:

http://es6.ruanyifeng.com/

## 5.邮箱的正则表达式

```jsx
/^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/		
/*只允许英文字母、数字、下划线、英文句号、以及中划线组成*/
/^[A-Za-z0-9\u4e00-\u9fa5]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/	
/*名称允许汉字、字母、数字，域名只允许英文域名*/
```
## 6.事件委托

- 事件委托就是利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。
- JavaScript中，添加到页面上的事件处理程序数量将直接关系到页面的整体运行性能，因为需要不断的与dom节点进行交互，访问dom的次数越多，引起浏览器重绘与重排的次数也就越多，就会延长整个页面的交互就绪时间，这就是为什么性能优化的主要思想之一就是减少DOM操作的原因；如果要用事件委托，就会将所有的操作放到js程序里面，与dom的操作就只需要交互一次，这样就能大大的减少与dom的交互次数，提高性能；

### 详情请参考:

http://www.cnblogs.com/leejersey/p/3801452.html

## 7.数组的方法

```javascript
var	arr1=[4,5,2,6,3];
var	arr2=[9,7,0,9];
arr1.concat(arr2);					//两个数组组合拼接
var str=arr1.join("-");			//用符号-连接数组每一项，得到字符串
str.split("-");					//把字符串中-每一段，分为数组每一项
arr1.reverse();					//倒序排列数组
function reFn(a,b){
  return (a-b);
}
arr1.sort(reFn);				//从小到大排序
arr1.splice(0,2,3,4);			//从索引0开始删除2个，再在删除的地方插入3,4，此方法会修改原数组
arr1.slice(0,2);				//从索引0开始，截取到索引2，[0,2)能取到0，取不到2
arr1.push(1);					//从数组arr1后面添加一项
arr1.pop();						//从数组arr1后面删除一项
arr1.unshift(1);				//从数组arr1前面添加一项
arr1.shift();					//从数组arr1前面删除一项
arr1.indexOf(2);				//从数组arr1中查找2，返回第一个2的索引，没有则返回-1
arr1.indexOf(2,1);				//从数组arr1中索引1开始查找2，返回第一个2的索引，没有则返回-1
arr1.lastIndexOf(2);			//从数组arr1中最后面开始查找2，返回第一个2的索引，没有则返回-1
arr1.findIndex(function(x) {
  return (x == 2);
});							//2	返回第一个符合条件的数组成员的位置
arr1.findIndex(function(value, index, arr) {  
	return value > 5;  
})							 // 3  返回第一个符合条件的数组成员的位置
var arrNew=arr1.filter(function(el,index,arr){
  	if(el>4){
      return false;
  	}
  	return true;
});								//数组筛选，返回true的保留
arr1.forEach(function(el,index,arr){
  	console.log(el);
});								//数组遍历
var arrNew = arr1.map((currentValue, index, array) => {
    console.log(`currentValue = `, currentValue);
    console.log(`index = `, index);
    console.log(`array= `, array);
    return currentValue * 2;
}, arr1);	//对数组每一项进行遍历操作，最后一个参数arr1（可选），表示回调函数中this指向
arr1.find((n) => n < 4);		//2	 找出第一个符合条件的数组成员
arr1.find(function(value, index, arr) {  
	return value >4;  
}) // 5   找出第一个符合条件的数组成员
arr1.every(function(e){
  return (e>5);
});		//false  检测数组所有元素是否都符合指定条件
arr1.every(function(e){
  return (e>5);
});		//true  用于检测数组中的元素是否满足指定条件,有一个就可以
```

## 8.字符串方法

```javascript
var str="hello world";
str.slice(4,7);             //o w  起始位置和结束位置(不包括结束位置)
str.substring(4,7);         //o w	起始位置和结束位置(不包括结束位置)
str.substring(7,4);         //o w	较小的为起始位置，较大的为结束位置
str.substr(4,7);            //o world  起始位置和所要返回的字符串长度
str.search('ll');			//2	检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串
//--------------------------------------------
str.slice(-3);              //rld	将它字符串的长度与对应的负数相加，结果作为参数
str.slice(3,-4);       		//lo w 将它字符串的长度与对应的负数相加，结果作为参数

str.substring(-3);     		//hello world	将负参数都直接转换为0
str.substring(3,-4);   		//hel	将负参数都直接转换为0

str.substr(-3);        		//rld	将第一个参数与字符串长度相加后的结果作为第一个参数
str.substr(3,-4);      		//空字符串	将第一个参数与字符串长度相加后的结果作为第一个参数
//-----------------------------------------------------------------
str.indexOf("e");			//1 第一个匹配的字符串索引位置
str.replace("o","!");		//只会替换第一个匹配的o字符串替换为！
str.replace(/o/g,"!");		//替换所有匹配的o字符串替换为！
str.charAt(2);				//l 指定索引位置2处的字符
var str2=str.toUpperCase();	//HELL0 WORLD 变成大写字符串
str2.toLowerCase();			//hello world 变成小写字符串
```

## 9.fetch请求超时处理

```javascript
//方法一：单纯setTimeout方式
var oldFetchfn = fetch; //拦截原始的fetch方法
window.fetch = function(input, opts){//定义新的fetch方法，封装原有的fetch方法
    return new Promise(function(resolve, reject){
        var timeoutId = setTimeout(function(){
            reject(new Error("fetch timeout"))
        }, opts.timeout);
        oldFetchfn(input, opts).then(
            res=>{
                clearTimeout(timeoutId);
                resolve(res)
            },
            err=>{
                clearTimeout(timeoutId);
                reject(err)
            }
        )
    })
}
//方法二：利用Promise.race方法
var oldFetchfn = fetch; //拦截原始的fetch方法
window.fetch = function(input, opts){//定义新的fetch方法，封装原有的fetch方法
    var fetchPromise = oldFetchfn(input, opts);
    var timeoutPromise = new Promise(function(resolve, reject){
        setTimeout(()=>{
             reject(new Error("fetch timeout"))
        }, opts.timeout)
    });
    retrun Promise.race([fetchPromise, timeoutPromise])
}
```

### 详情请参考:

http://www.cnblogs.com/huilixieqi/p/6494380.html

## 10.下面执行结果

```javascript
var num = +{
  name:'ls',
  age:13,
  sayHello:function(){
    console.log(this.name+'----'+this.age)
  }
}
console.log(num)
```

#### 结果：NAN

## 11.js闭包的理解

- #### 闭包就是能够读取其他函数内部变量的函数。

- #### 闭包的用途

  一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。

- #### **闭包的注意点**

  - 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
  - 闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。

### 详情请参考:

http://www.cnblogs.com/wangfupeng1988/p/3994065.html

http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html

http://www.cnblogs.com/yunfeifei/p/4019504.html

## 12.this的指向问题

- #### 1.方法调用模式 

  当一个函数被保存为对象的一个属性时, 我们称它为一个方法, 当一个方法被调用时, this指向该对象

- #### 2.函数调用模式 （或全局）

  当一个函数并非一个对象的属性时, 它被当作一个函数来调用, 此时的this指向全局对象(window)

- #### 3.构造器调用模式

  结合new前缀调用的函数被称为构造器函数, 此时的this指向该构造器函数的实例对象

- #### 4.apply/call调用模式

  apply和call方法可以让我们设定调用者中的this指向谁

### 详情请参考:

http://blog.csdn.net/babybk/article/details/51272790

## 13.定时器里面this指向问题

- #### setTimeout函数中的this会指向window对象

```jsx
var num = 0;
function Obj (){
    this.num = 1,
    this.getNum = function(){
        console.log(this.num);
    },
    this.getNumLater = function(){
        setTimeout(function(){
            console.log(this.num);
        }, 1000)
    }
}
var obj = new Obj; 
obj.getNum();//1　　打印的是obj.num，值为1
obj.getNumLater()//0　　打印的是window.num，值为0
```

从上述例子中可以看到setTimeout中函数内的this是指向了window对象，这是由于`setTimeout()调用的代码运行在与所在函数`完全分离的执行环境上。这会导致这些代码中包含的 `this` 关键字会指向 `window` (或`全局`)对象

- #### setTimeout(this.method, time)这种形式中的this，即上文中提到的第一个this，是根据上下文来判断的，默认为全局作用域，但不一定总是处于全局下，具体问题具体分析。

  ```jsx
  var value=33;
  function Foo() {
      this.value = 42;
      this.method = function() {
          // this 指向全局对象
          alert(this)   // 输出window    第二个this
          alert(this.value); // 输出：33   第二个this
      };
      setTimeout(this.method, 500);  // 这里的this指向Foo的实例对象  第一个this
  }
  new Foo();
  ```

- #### 利用bind()方法

  ```jsx
  var num = 0;
  function Obj (){
      this.num = 1,
      this.getNum = function(){
          console.log(this.num);
      },
      this.getNumLater = function(){
          setTimeout(function(){
              console.log(this.num);
          }.bind(this), 1000)    //利用bind()将this绑定到这个函数上
      }
  }
  var obj = new Obj; 
  obj.getNum();//1　　打印的为obj.num，值为1
  obj.getNumLater()//1　　打印的为obj.num，值为1
  ```

bind()方法是在Function.prototype上的一个方法，当被绑定函数执行时，bind方法会创建一个新函数，并将第一个参数作为新函数运行时的this。在这个例子中，在调用setTimeout中的函数时，bind方法创建了一个新的函数，并将this传进新的函数，执行的结果也就是正确的了。

- #### 箭头函数

  ```jsx
  var num = 0;
  function Obj (){
      this.num = 1,
      this.getNum = function(){
          console.log(this.num);
      },
      this.getNumLater = function(){
          setTimeout(() => {
              console.log(this.num);
          }, 1000)    //箭头函数中的this总是指向外层调用者，也就是Obj
      }
  }
  var obj = new Obj; 
  obj.getNum();//1　　打印的是obj.num，值为1
  obj.getNumLater()//1　　打印的是obj.num，值为1
  ```

ES6中的箭头函数完全修复了this的指向，this总是指向词法作用域，也就是外层调用者obj，因此利用箭头函数就可以轻松解决这个问题。

### 详情请参考:

http://www.cnblogs.com/zsqos/p/6188835.html

http://www.cnblogs.com/hutaoer/p/3423782.html

## 14.js框架封装

#### 模拟jQuery框架，利用原生的js技术，封装一个js框架，以加深对jQuery的常用api的使用和面向对象原理的理解；

#### 一：结构部分

首先利用闭包，构造一个自执行函数，然后利用选择器函数Sizzle，获取dom元素；其后设置入口函数jQuery，返回一个F的实例；
然后对jQuery.prototype进行设置；其后修改F的原型指向jQuery的原型,最后暴露出去两个接口$和jQuery；

#### 二：jQuery.fn.extend = jQuery.extend = function(){}

通过向jQuery的原型和jQuery上添加一个extend方法；
可以实现扩展工具类方法和dom操作、css操作类的方法；
jQuery.fn.extend(object); 对jQuery.fn即jQuery.prototype
得扩展，就是为jQuery类添加“成员函数”。jQuery类的实例可以使用这个“成员函数”。

### 详情请参考:

http://www.cnblogs.com/marsqi/p/6280429.html