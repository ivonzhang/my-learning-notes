> ### let和const命令

  - var：声明变量，更多的是全局作用域，存在变量提升
  - let：声明变量，存在于块级作用域，不会变量提升（如适用于for循环中做计数器）
  - const：声明常量，只在声明所在的块级作用域内有效，const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动 

> ### 变量的解构赋值

   ES6按照模式匹配，从** 数组 **和** 对象 **中按照属性名称提取值，对变量进行赋值。
  - 数组的解构：
        let [x, y] = [1, 2, 3];
        x // 1
        y // 2 
    - 事实上，只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值，如Set集合：
           let [x, y, z] = new Set(['a', 'b', 'c']);
           x // "a" 
    - 解构赋值允许指定默认值：
          let [foo = true] = [];
          foo // true

          let [x, y = 'b'] = ['a']; // x='a', y='b'
          let [x, y = 'b'] = ['a', undefined]; // x='a', y='b' 
    - 如果解构不成功，变量的值就等于undefined：
          let [foo] = [];
          let [bar, foo] = [1];
          foo//undefined 

  - 对象的解构赋值
        let { foo, bar } = { foo: "aaa", bar: "bbb" };
        foo // "aaa"
        bar // "bbb"  
  区别：
  1) 数组的元素是按次序排列的，变量的取值由它的位置决定；
  2) 对象的属性没有次序，变量必须与属性同名，才能取到正确的值 
        let { baz } = { foo: "aaa", bar: "bbb" };
        baz // undefined  
    - 对象的解构赋值的内部机制：先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。
          let obj = { first: 'hello', last: 'world' };
          let { first: f, last: l } = obj;
          f // 'hello'
          l // 'world'

      > 上面代码中，first和last是匹配的模式，f和l才是变量。真正被赋值的是变量f和l，而不是模式first和last。
    - 对象的解构也可以指定默认值 (** 默认值生效的条件是，对象的属性值严格等于undefined **)
          var {x = 3} = {};
          x // 3

          var {x, y = 5} = {x: 1};
          x // 1
          y // 5 
          
          // 属性值为undefined
          var {x = 3} = {x: undefined};
          x // 3

          var {x = 3} = {x: null};
          x // null

  - 字符串的解构赋值  
      
        const [a, b, c, d, e] = 'hello';
        a // "h"
        b // "e"
        c // "l"
        d // "l"
        e // "o" 

  - 数值和布尔值的解构赋值 

    解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。

  - 函数参数的解构赋值  
        function add([x, y]){
          return x + y;
        }

        add([1, 2]); // 3 

  - 用途
    - （1）交换变量的值 
          let x = 1;
          let y = 2;

          [x, y] = [y, x]; 

    - （2）从函数返回多个值
          // 返回一个数组
          function example() {
            return [1, 2, 3];
          }
          let [a, b, c] = example(); 

    - （3）函数参数的定义：
          // 参数是一组有次序的值
          function f([x, y, z]) { ... }
          f([1, 2, 3]);

          // 参数是一组无次序的值
          function f({x, y, z}) { ... }
          f({z: 3, y: 2, x: 1});

    - （4）提取JSON数据：
          let jsonData = {
              id: 42,
              status: "OK",
              data: [867, 5309]
          };

          let { id, status, data: number } = jsonData;

          console.log(id, status, number);
          // 42, "OK", [867, 5309] 

    - （5）函数参数的默认值 

    - （6）遍历Map结构 
          var map = new Map();
          map.set('first', 'hello');
          map.set('second', 'world');

          for (let [key, value] of map) {
            console.log(key + " is " + value);
          }
          // first is hello
          // second is world
          
          // 获取键名
          for (let [key] of map) {
            // ...
          }

          // 获取键值
          for (let [,value] of map) {
            // ...
          } 

    - （7）输入模块的指定方法

      加载模块时，往往需要指定输入哪些方法。解构赋值使得输入语句非常清晰。
          const { SourceMapConsumer, SourceNode } = require("source-map");  

> ### 字符串的扩展


![Paste_Image.png](http://upload-images.jianshu.io/upload_images/5307186-d5f097fef1f0dab1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 模板字符串 
    是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。 
      // 普通字符串
      `In JavaScript '\n' is a line-feed.`

      // 多行字符串
      `In JavaScript this is
       not legal.` 
      
       // 字符串中嵌入变量
      var name = "Bob", time = "today";
      `Hello ${name}, how are you ${time}?`

> ### 数值的扩展

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/5307186-e84b21d0ce941b33.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)　


  - 二进制和八进制
    ES6 提供了二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示。

        0b111110111 === 503 // true
        0o767 === 503 // true 

  - 指数运算符 
    ES2016 新增了一个指数运算符（**）

        2 ** 2 // 4
        2 ** 3 // 8

> ### 数组的扩展

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/5307186-df03d1b12e896e92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  - Array.from
  Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。 
           let arrayLike = {
              '0': 'a',
              '1': 'b',
              '2': 'c',
              length: 3
          };

          // ES5的写法
          var arr1 = [].slice.call(arrayLike); // ['a', 'b', 'c']

          // ES6的写法
          let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']


> ### 函数的扩展 


![Paste_Image.png](http://upload-images.jianshu.io/upload_images/5307186-7701b86c107f824f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  - 箭头函数
    ES6允许使用“箭头”（=>）定义函数。
            var f = () => 5;
            // 等同于
            var f = function () { return 5 };

            var sum = (num1, num2) => num1 + num2;
            // 等同于
            var sum = function(num1, num2) {
              return num1 + num2;
            };

  - rest参数
    形式为“...变量名”。用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。 
        function add(...values) {
          let sum = 0;
          //  valuses数组
          for (var val of values) {
            sum += val;
          }

          return sum;
        }

        add(2, 5, 3) // 10

  - 扩展运算符** ... **
    扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。 
        console.log(...[1, 2, 3])
        // 1 2 3

        console.log(1, ...[2, 3, 4], 5)
        // 1 2 3 4 5

        [...document.querySelectorAll('div')]
        // [<div>, <div>, <div>]

> ### Symbol

 ES6为了防止属性名的冲突，引入了一种新的原始数据类型Symbol，表示独一无二的值。它是JavaScript语言的第七种数据类型。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的Symbol类型。 

> ### Set和Map数据结构　

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/5307186-62520d815de82663.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

  - Set
    类似于数组，但是成员的值都是唯一的，没有重复的值。 
        // 例一
        var set = new Set([1, 2, 3, 4, 4]);
        [...set]
        // [1, 2, 3, 4]

        // 例二
        var items = new Set([1, 2, 3, 4, 5, 5, 5, 5]);
        items.size // 5

  - Map
    类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。
        var m = new Map();
        var o = {p: 'Hello World'};

        m.set(o, 'content')
        m.get(o) // "content"

        m.has(o) // true
        m.delete(o) // true
        m.has(o) // false

> ### Promise对象

Promise 是异步编程的一种解决方案，比传统的解决方案回调函数和事件更合理和更强大。 

        var promise = new Promise(function(resolve, reject) {
          // ... some code

          if (/* 异步操作成功 */){
              resolve(value);
          } else {
            reject(error);
          }
        });
Promise还可以做更多的事情，比如，有若干个异步任务，需要先做任务1，如果成功后再做任务2，任何任务失败则不再继续并执行错误处理函数。
要串行执行这样的异步任务，不用Promise需要写一层一层的嵌套代码。有了Promise，我们只需要简单地写： 

     job1.then(job2).then(job3).catch(handleError); 
> 注意执行顺序：Promise实例新建后立即执行——>然后执行当前脚本所有同步任务——>执行完才会执行then方法指定的回调函。　　　　

　

> ### Generator

Generator 函数是 ES6 提供的一种异步编程解决方案。Generator 函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield语句，定义不同的内部状态。

    function* helloWorldGenerator() {
      yield 'hello';
      yield 'world';
      return 'ending';
    }

    var hw = helloWorldGenerator(); 
    hw.next()
    // { value: 'hello', done: false }

    hw.next()
    // { value: 'world', done: false }

    hw.next()
    // { value: 'ending', done: true }

    hw.next()
    // { value: undefined, done: true }  

> ### class


![Paste_Image.png](http://upload-images.jianshu.io/upload_images/5307186-f85bf0627b3d7503.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 
ES6定义一个类，如下：

    //定义类
    class Point {
      constructor(x, y) {
        this.x = x;
        this.y = y;
    }

      toString() {
        return '(' + this.x + ', ' + this.y + ')';
      }
    }  

  - class继承
    Class之间可以通过extends关键字实现继承：
        class ColorPoint extends Point {
          constructor(x, y, color) {
            super(x, y); // 调用父类的constructor(x, y)
            this.color = color;
          }

          toString() {
            return this.color + ' ' + super.toString(); // 调用父类的toString()
          }
        }

> ### 模块module

模块功能主要由两个命令构成：export和import。export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。

  - export default 命令
  - 模块的继承 
  - 跨模块常量
        // constants.js 模块
        export const A = 1;
        export const B = 3;
        export const C = 4;

        // test1.js 模块
        import * as constants from './constants';
        console.log(constants.A); // 1
        console.log(constants.B); // 3