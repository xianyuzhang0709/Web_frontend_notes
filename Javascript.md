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

**主流浏览器：**IE，Chrome，Firefox，Opera，Safari等（必须有独立研发的内核才能算）。

| 主流浏览器 |     内核     |
| :--------: | :----------: |
|     IE     |   trident    |
|   Chrome   | webkit/blink |
|  Firefox   |    Gecko     |
|   Opera    |    presto    |
|   Safari   |    webkit    |

### JS特点：

1. 解释型语言 —— 跨平台；

2. 单线程（但能呈现同步执行的运行效果）；

3. ECMA标准 —— 定义了JS的统一标准。

4. case-sensitive. 大小写敏感。所以：只有true，没有True

   ```javascript
   typeof(true);     //boolean 
   typeof(True);     //undefined
   
   typeof(-Infinity);//-Infinity
   typeof(infinity); //undefined
   ```

### JS三阶段：

原生JS叫**ECMAScript**，只能提供数组的处理等功能。

浏览器提供给js的功能，**DOM**和**BOM**。

* DOM操作文档，HTML+CSS；BOM操作浏览器。

# ECMAScript - 原生JS

### 基本语法：

1. 变量（variable）

   ```javascript
   var a;      //变量声明
   a = 100;    //赋值
   
   var a = 10, //(逗号)
       b = 20,
       c;      //同时声明多个变量
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
     var a = 123;                   //1. number
     var b = "";                    //2. string
     var c = true;                  //3. boolean (注意true、false都是小写)
     var d;                         //4. undefined.声明未赋值，typeof(d)是undefined;
     var e = null;                  //5. 占位(typeof(e)是object)
     
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
   * 隐式类型转换：不能用`+`运算的，先number()，再运算

   ```javascript
   var a = "a"+1+1;       //a == "a11"
   var b = 1+1+"a"+1;     //b == "2a1";
   ```

2. `/`

   ```javascript
   var a = 1/0;           //a == Infinity
   var b = -1/0;          //b == -Infinity
   var c = 0/0;           //c == NaN
   var d = 1/Infinity;    //d == 0
   var e = 1/-Infinity;   //d == -0
   typeof(-0);            //number
   ```

   

### JS运算符：

运算必然有输出结果。

1. 比较运算符：`>  <  >=  <=  ==  !=` 输出结果为**boolean值**。

   ```javascript
   //>  <  >=  <=
   var a = "a" > "b"               //false;
   var a = "1" > "8"               //false;
   var a = "feng" > "deng"         //true;
   
   //== 等于
   var a = undefined == undefined; //true
   var a = Infinity == Infinity;   //true
   var a = NaN == NaN;             //false（NaN不等于任何数，包括自己）
   ```

   * `> <` ：字符串相比时，是其首字母的ascii码相比较

2. 逻辑运算符：`&&  ||  !` 输出结果为**真实值**。

   ```javascript
   //&& 且
   //左→右，依次判断，遇到false就返回该表达式的值，全为true时，返回最后一个表达式的值。
   var a = 1 && 2+2;               //4
   var a = 0 && 2+2;               //0
   
   //|| 或
   //左→右，依次判断,只要发现true，就返回该表达式的值。
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
typeof();                  //报错：Unexpected token ')'
typeof(123);               //1 number
typeof(true);              //2 boolean
typeof("");                //3 string
typeof(undefined);         //4 undefined
typeof(null);              //5 object
typeof([1,2,3]);           //6 object    //(array)
typeof({});                //7 object    //(object)
typeof(function(){});      //8 function  //function)
typeof(for(){});           //报错
typeof(typeof(1));         //string
```

* typeof()一共可输出6种type：number, boolean, string, undefiend, object, function.
* 1 - 5原始值，6 - 8引用值。

1. **Number(mix)** - Convert different object values to their numbers。（整个值是数字，或整体具有数字意义才可以转）

   ```javascript
   Number();               //==0      (空)
   Number(123);            //==123    (number)
   Number(-Infinity);      //==-Infinity    (number - Infinity)
   Number(NaN);            //==NaN    (number - NaN)
   Number("456");          //==456    (string是纯数字的，可以转为数字，否则NaN)
   Number("1,2,3")         //==NaN    (string，不具备数学意义)
   Number("100abc");       //==NaN    (string)
   Number("");             //==0      (string - 空串)
   Number("  ");           //==0      (string - 带空格的空串)
   Number(true);           //==1      (boolean)
   Number(undefined);      //==NaN    (未赋值)
   Number([1,2,3]);        //==NaN    (array)
   Number({});             //==NaN    (object)
   Number(null);           //==0
   Number(function(){});   //==NaN  (function)
   ```

   * 以上输出结果，typeof()都是number。

2. **parseInt(string, radix)** - 将一个字符串 string，以 radix（2-36）进制为基底，转为十进制integer。（第一个字符是number就是可以转）

   ```javascript
   parseInt();     	    	//==NaN    (空)
   parseInt(123);  	    	//==123    (number)
   parseInt(-Infinity);    //==NaN    (number - Infinity)
   parseInt(NaN);  		    //==NaN    (number - NaN)
   parseInt("456");        //==456    (string是纯数字的，可以转为数字，否则NaN)
   parseInt("100abc");     //==100    (string - 开头有数字)
   parseInt("a100bc");     //==NaN    (string - 开头无数字)
   parseInt("");           //==NaN    (string - 空串)
   parseInt(true);         //==NaN    (boolean)
   parseInt(undefined);    //==NaN    (未赋值)
   parseInt([1.9,2,3]);    //==1      (array)
   parseInt({});				    //==NaN    (object)
   parseInt(null);         //==NaN
   parseInt(function(){}); //==NaN  (function)
   ```

   * 如果radix没有，则默认开头为0x是十六进制；开头0是八进制，开头其他数字，则为十进制。
   * 如果the first character 不能 converted to a number, then return NaN。
   * 即，能转为整数的有：数字，字符串开头是数字的，array开头是数字的。看到数字位，遇到点停止。

   * parseInt向下取整。`Math.floor()`向下取整，`Math.ceil()`向上取整，`Math.round()`四舍五入取整。

3. **parseFloat(string)** - 识别到最后一个数字位，且只能识别一个点。

   ```javascript
   parseFloat("1.2.4flos");   //==1.2  typeof(a)==number
   parseFloat(-Infinity);     //==-Infinity
   parseFloat("456abc");      //==456
   parseFloat("a100bc");      //==NaN
   parseFloat([1.9,2,3]);     //==1.9
   ```

4. **String(mix)** - 把一切都转化成string

   ```javascript
   var a = String([1,2,3]);     //1,2,3
   var b = String(function(){});//function(){}
   var c = String(Infinity);    //Infinity
   var d = String(null);        //null
   var f = String();            //
   var g = String("");          //
   var demo = null + "";        //任何东西+空串，都可以返回其string形式
   ```

5. **Boolean()** - 转化成boolean

   ```javascript
   var a = Boolean([1,2,3]);     //true
   var b = Boolean(function(){});//true
   var c = Boolean(Infinity);    //true
   var d = Boolean(null);        //false
   var f = Boolean();            //false
   var g = Boolean("");          //false
   ```

6. **.toString(radix)** - 返回一个该对象的字符串，radix是目标进制。将对象以十进制转化为radix进制。

   ```javascript
   var demo = [1,2,3];
   var d = demo.toString();      //1,2,3
   
   //以下省略demo.toString():
   var demo = {};                //[object Object]
   var demo = undefiend;         //报错
   var demo = null;              //报错
   //一般用String()来做字符串操作，或+""，也可以转化为string。
   ```

   进制转换：

   ```javascript
   var a = 20;
   var b = a.toString(8);         //24(8进制)
   
   //n进制 → 十进制: parseInt(string, radix);
   //十进制 → n进制: toString(radix);
   //例：2进制 to 16进制
   var a = 10000;                 //a == 二进制10000
   var b = parseInt(a, 2);        //b == 十进制16
   var c = b.toString(16);        //c == 十六进制10
   ```

### 隐式类型转换：

1. **isNaN()** - 确定一个值是不是NaN。

   * 不是number的通过Number()转化为number，再判断。

   ```javascript
   isNaN(NaN);       // true
   isNaN(undefined); // true
   isNaN({});        // true
   
   isNaN(true);      // false
   isNaN(null);      // false
   isNaN(37);        // false
   
   // strings
   isNaN("37");      // false: 可以被转换成数值37
   isNaN("37.37");   // false: 可以被转换成数值37.37
   isNaN("37,5");    // true: 不能转化成37
   isNaN('123ABC');  // true:  parseInt("123ABC")的结果是 123, 但是Number("123ABC")结果是 NaN
   isNaN("");        // false: 空字符串被转换成0
   isNaN(" ");       // false: 包含空格的字符串被转换成0
   
   // dates
   isNaN(new Date());                // false
   isNaN(new Date().toString());     // true
   
   isNaN("blabla")   // true: "blabla"不能转换成数值
                     // 转换成数值失败， 返回NaN
   ```

2. **`++  --  +(正) -(负)`**： 先用Number()转化

3. **`+(加号)`**：左右只要有string，整个都变成string。

4. **`-(减号) *(乘号) /(除号) %(余)`**：先Number()

5. **&& || !**：判断用true/false判断，结果将对应表达式的**值**输出。

6. **`> < >= <=`**：有number比较，则number优先，把两边都换成数字比；字符串则首字母ascii码比。

   ```javascript
   var a = "3" > 2;   //true
   var a = "3" > "2"; //false
   
   var a = 10 > 5 > 3;//false, 从左到右判断，10>5返回true，true==1, 1>3则为false
   ```

7. `== !==` ：也有类型转换。

   ```javascript
   undefined > 0      //false
   undefined < 0      //false
   undefined == 0     //false
   
   null > 0           //false
   null < 0           //false
   null == 0          //false
   
   undefined == null  //true
   
   NaN == NaN         //false，NaN不等于任何，包括自己
   ```

8. 不发生类型转换的：绝对等于`===`和绝对不等于`!==`

9. 报错：未定义的变量进行使用——必然报错；当且仅当typeof(未定义variable)时不报错。
   * typeof(typeof(a)) == typeof("undefiend") == string
   * num.toFix(3) 意思是，把num四舍五入，小数点后保留3位有效数字。

### 函数function(){}