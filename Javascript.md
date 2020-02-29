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

### js特点：

解释型语言 —— 跨平台；

单线程（但能呈现同步执行的运行效果）；

ECMA标准 —— 定义了JS的统一标准。

[1]: Web_frontend_notes/Js_reference.md###解释性语言？	"什么是解释型语言"

### js三阶段：

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
   		b = 20，
       c; //同时声明多个变量
   ```

   * 变量命名规则：
     * 开头：英文字母、_ 、$
     * 中间：英文字母、_ 、$ 、数字
     * （不可用：关键字，保留字）

2. 值类型（Type of JavaScript）

   * 原始值（栈数据）- primitives types - **immutable** 不可改变

     * Number, String, Boolean, undefined, null （5种）

   * 引用值（堆数据） - Composite data type 复合型

     * Array, object, function （3种）（没有list)

   * 定义：

     ```javascript
     var b = "";           //String
     var c = true;//false  //Boolean
     var d;                //undefined.声明未赋值，typeof(d)=undefined;
     var e = null;         //占位(null是object)
     
     var arr = [1,2,3,false,"abc"]  //Array
     var obj = {										 //Object
       name : "xiaoliu",
       age  :  16,
       health: function(){
         age--;
       }
     }
     function abc(){					//function
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
     arr = [1,3];  //arr被重新赋值，并没有在堆中改变原值，而是在堆中以一个新的存错单元所存的值，赋值给arr，arr保留其地址。
     //所以, arr = [1,2]，而arr1 = [1,3]
     ```

     ![arr2](imgs/array_type_core2.png)

     

