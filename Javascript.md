# JavaScript:

**历史**：js曾是Netscape Navigator浏览器的一部分首次出现于1996年，最初设计目的是改善用户浏览网页的体验。

**作者**：Brendan Eich

期初js名为LiveScript，后与Sun公司合作，改名JavaScript，之后Sun被Oracle收购，js版权归Oracle所有。

### **浏览器的组成：**

**shell**：用户能操作的部分，eg：设置，edit，help等；

**内核**：看不到的，能够处理代码，并把代码结果运算和显示出来的就是内核。（运行能力）

* 渲染引擎（语法规则和渲染）：即绘制，根据HTML和CSS语法的识别，类似3D，帧频16ms；
* js引擎：负责JavaScript；
* 其他引擎：负责异步等。

**Chrome浏览器**优化js引擎，命名为**V8**，直接把js转化为用机器码来执行，速度极快。

**Firefox3.5** TraceMonkey（对频繁执行的代码做了路径优化）

**Firefox4.0** leagerMonkey

**主流浏览器：**

| 主流浏览器 |     内核     |
| :--------: | :----------: |
|     IE     |   trident    |
|   Chrome   | webkit/blink |
|  Firefox   |    Gecko     |
|   Opera    |    presto    |
|   Safari   |    webkit    |

IE，Chrome，Firefox，Opera，Safari等（必须有独立研发的内核）。

### JS特点：

解释型语言 —— 跨平台；

单线程（但能呈现同步执行的运行效果）；

ECMA标准 —— 定义了JS的统一标准。

[1]: Js_reference.md	"什么是解释型语言"

case-sensitive. 大小写敏感。所以：只有true，没有True

```javascript
typeof(true);//-->boolean 
typeof(True);//-->undefined

typeof(-Infinity);//-->-Infinity
typeof(infinity);//-->undefined
```



### JS三阶段：

原生JS叫**ECMAScript**，只能提供数组的处理等功能。

浏览器提供给js的功能，**DOM**和**BOM**。

* DOM操作文档，HTML+CSS；BOM操作浏览器。

# ECMAScript - 原生JS

### 基本语法：

1. 变量（variable）

   ```javascript
   var a; //变量声明
   a = 100; //赋值
   
   var a = 10, //逗号
       b = 20,
       c; //同时声明多个变量
   ```

   * 变量命名规则：
     * 开头：英文字母、_ 、$
     * 中间：英文字母、_ 、$ 、数字
     * （不可用：关键字，保留字）

2. 值类型（Type of JavaScript）

   * 原始值（栈数据）- primitives types - **immutable** 不可改变

     * number, string, boolean, undefined, null （5种）
     * （number中包含NaN，Infinity，-Infinity三个特殊值）

   * 引用值（堆数据） - Composite data type 复合型

     * Array, object, function （3种）（没有list)

   * 定义：

     ```javascript
     var a = 123;          //1. number
     var b = "";           //2. string
     var c = true;//false  //3. boolean (注意都是小写)
     var d;                //4. undefined.声明未赋值，typeof(d)是undefined;
     var e = null;         //5. 占位(typeof(e)是object)
     
     var arr = [1,2,3,false,"abc"]  //6. Array，typeof(arr)是object, 使用arr.isArray来判断数组
     var obj = {                    //7. Object
       key  : values,//注意是逗号
       name : "xiaoliu",
       age  :  16,
       health: function(){
         age--;
       }
     }
     function abc(){                //8. function
       var a = 2;
     }
     ```

   * 引用值（堆数据）的特殊性：

     原始值存在栈中，数据复制/更改，都在栈中进行。

     ![num_type](imgs/num_type_core1.png)

     而引用值（堆数据），例如arr，在栈中存放了其值[1,2]所在的堆中的地址。

     ```javascript
     var arr = [1,2];
     var arr1 = arr;
     arr.push(3);
     //此时arr1也变成[1,2,3]。
     ```

     ![array_type](imgs/array_type_core1.png)

     ```javascript
     var arr = [1,2];
     var arr1 = arr;
     arr = [1,3];  
     //arr被重新赋值，并没有在堆中改变原值，而是在堆中以一个新的存错单元所存的值，赋值给arr，arr保留其地址。
     //所以, arr = [1,2]，而arr1 = [1,3]
     ```

     ![arr2](imgs/array_type_core2.png)

     

# 基本语法：

1. 语句以“；”结束。
2. js语法错误会导致后续代码终止，但不影响其他js代码块/文件。
3. 书写规范，“=+/-”两边都有空格。

```javascript
function test(){}

if(condition){  //条件为true时执行
  	statements;
}else if(condition){
  	statements;
} 

//while循环
while (condition){
  	statements;
}
//do while
do{
  	statements;
}while()

//switch case       
switch(expression) {
    case x:
      statements x;
      break; //不加break的话，语句会把正确的语句执行后，返回后续值
    case y:
      statements y;
      break;
    default:
      statements d;
}

//The break - "jumps out" of a loop.
//The continue - "jumps over" one iteration in the loop.

//for循环
for (initialExpression; condition; incrementExpression){
  	statements;
}

//for...in 语句
for (variable in object) {
  	statements
}  

// for...of 语句
for (variable of object)
  	statement
//不同：for...in iterates over property names, for...of iterates over property values. 
//for...in通过属性名来迭代；for...of通过属性值来迭代。

//输入
var score = parseInt(window.prompt("input:"));
//输出
document.write(score);
console.log(score);
```

### 一、运算操作符：

* `+  -  *  /  %  =  ()`  优先级`=`最弱，`()`最高。
* `++  --`  a++，先执行语句后+1；++a，先+1后执行语句。
* ` +=  -=  /=  *=  %=`

1.  `+` （自左向右）
   * 数学运算、字符串连接
   * 任何数据类型 + 字符串 = 字符串
   * 隐式：不能运算的，先number()，再运算
     * `"a"+1+1` ---> `"a11"`
     * `1+1+"a"+1` ---> `"2a1"`

2. `/`
   + `1/0` ---> `Infinity` （Infinity是number）
   + `-1/0` ---> `-Infinity`
   + `0/0` ---> `NaN`  (NaN是number)



### JS运算符：

运算必然有输出结果。

1. 比较运算符：`>  <  >=  <=  ==  !=` 输出结果为**boolean值**。

   ```javascript
   //>  <  >=  <=
   var a = "a" > "b" //---> a为false;
   var a = "1" > "8" //---> a为false;
   var a = "feng" > "deng" //---> true.
   
   //== 等于
   var a = undefined == undefined; //true
   var a = Infinity == Infinity; //true
   var a = NaN == NaN; //false（NaN不等于任何数，包括自己）
   ```

   * `> <` ：字符串相比时，是其首字母的ascii码相比较

2. 逻辑运算符：`&&  ||  !` 输出结果为**真实值**。

   ```javascript
   //&& 且
   //左→右，依次判断,全为true时，返回最后一个表达式的值。
   var a = 1 && 2+2; //4
   var a = 0 && 2+2; //0  第一个表达式为false，返回第一个表达式的值。
   
   //|| 或
   //左→右，依次判断,只要发现true，返回该表达式的值。
   ```

   ```javascript
   //应用延伸：
   //1.用&&短路语句：
   var data = ...;
   data && fn(data) //如果data成功接收，则执行后面的function，比if写法更方便
   
   //2.用||写兼容：
   div.onclick = function(e){
     //e表示一个事件对象
     //非IE浏览器，直接用e就可以读取，但IE中，必须用window.event
     var event = e || window.event;
   }
   ```

3. 转换为boolean都是False的值：

   1. `undifined`
   2. `null`
   3. `""`（空串）
   4. `0`
   5. `false`

### typeof()和类型转换

```javascript
typeof();             //报错：Unexpected token ')'
typeof(123);          //1 number
typeof(true);         //2 boolean
typeof("");           //3 string
typeof(undefined);    //4 undefined
typeof(null);         //5 object
typeof([1,2,3]);      //6 object    //(array)
typeof({});           //7 object    //(object)
typeof(function(){}); //8 function  //function)
typeof(for(){});      //报错
typeof(typeof(1));    //string
```

* 1 - 5原始值，6 - 8引用值。

1. **Number(mix)** - Convert different object values to their numbers。

   ```javascript
   Number();         //==0      (空)
   Number(123);      //==123    (number)
   Number(-Infinity);//==-Infinity    (number - Infinity)
   Number(NaN);  		//==NaN    (number - NaN)
   Number("456");    //==456    (string是纯数字的，可以转为数字，否则NaN)
   Number("100abc"); //==NaN    (string)
   Number("");       //==0      (string - 空串)
   Number(true);     //==1      (boolean)
   Number(undefined);//==NaN    (未赋值)
   Number([1,2,3]);  //==NaN    (array)
   Number({});       //==NaN    (object)
   Number(null);     //==0
   Number(function(){});//==NaN  (function)
   ```

   * 以上输出结果，typeof()都是number。

2. **parseInt(string, radix)** - 将一个字符串 string 转换为 radix 进制的整数， radix 为介于2-36之间的数。

   ```javascript
   parseInt();     		//==NaN    (空)
   parseInt(123);  		//==123    (number)
   parseInt(-Infinity);//==NaN    (number - Infinity)
   parseInt(NaN);  		//==NaN    (number - NaN)
   parseInt("456");    //==456    (string是纯数字的，可以转为数字，否则NaN)
   parseInt("100abc"); //==100    (string - 开头有数字)
   parseInt("a100bc"); //==NaN    (string - 开头无数字)
   parseInt("");       //==NaN    (string - 空串)
   parseInt(true);     //==NaN    (boolean)
   parseInt(undefined);//==NaN    (未赋值)
   parseInt([1.9,2,3]);//==1      (array)
   parseInt({});				//==NaN    (object)
   parseInt(null);     //==NaN
   parseInt(function(){});//==NaN  (function)
   ```

   * 注意，能转为整数的有：数字，字符串开头是数字的，array开头是数字的。看到数字位，遇到点停止。

   * parseInt向下取整。`Math.floor()`向下取整，`Math.ceil()`向上取整，`Math.round()`四舍五入取整。
   * 以上输出结果，typeof()都是number。

3. parseFloat(string) - 识别到最后一个数字位，且只能识别一个点。

   ```javascript
   parseFloat("1.2.4flos"); //==1.2  typeof(a)==number
   parseFloat(-Infinity);   //==-Infinity
   parseFloat("456abc");    //==456
   parseFloat("a100bc");    //==NaN
   parseInt([1.9,2,3]);     //==1.9
   ```

   * 猜想：parseInt(string)的意思是不是先把内容转化成string，再Int。为了证明猜想，先看看toString()是怎么做的。

4. toString(radix) - 





