1. JS可以进行浮点计算。

   1. 计算 2 的 n 次幂，n 可输入，n 为自然数。
   2. 计算 n 的阶乘，n 可输入。即 5!=5*4*3*2*1，最好写个 if。
   3. 著名的斐波那契额数列（这个数列从第 3 项开始，每一项都等于前两项之和）1 1 2 3 5 8 输出第 n 项。
   4. 编写一程序，输入一个三位数的正整数，输出时反向输出。如:输入 456,输出 654。
   5. 输入 a,b,c 三个数字，打印出最大的。
   6. 打印出 100 以内的质数（从 1 除到他本身，只能有两个因数）

   ```javascript
   //1. 2的n次
   n = parseInt(window.prompt("input a number:"));
   var res = 1;
   for (var i = 0; i <n; i++){
   	res *= 2;
   }
   console.log(res);
   ```

   ```javascript
   //2. n的阶乘：5*4*3*2*1
   var n = parseInt(window.prompt("input a number:"));
   var res = n;
   for (var i = 1; i < n; i++){
   	res *= n-i;
   }
   console.log(res);
   
   //2.2 n的阶乘第二种方法：5*4*3*2*1 == 1*2*3*4*5
   var n = parseInt(window.prompt("input a number:"));
   var res = 1;
   for (var i = 1; i <= n; i++){
   	res *= i;
   }
   console.log(res);
   
   //2.3 递归
   var n = parseInt(window.prompt("input a number:"));
   function mul(n){
     if (n == 1){
       return 1;
     }
     return n * mul(n-1);
   }
   console.log(mul(n));
   ```

   ```javascript
   //3. 斐波那契额数列 - fsd每增加一个数就换一轮，n-2
   var n = parseInt(window.prompt("input a number:"));
   var f = 1;
   		s = 1;
   		d;
   if(n > 2){
     for (var i = 0; i < n - 2; i++){
       d = f + s;
       f = s;
       s = d;
     }
     console.log(d);//注意输出位置，for循环结束后，输出第n个fabonacci数。
   }else{
     console.log(1);
   }
   
   //3.2 递归fabonacci：
   var n = parseInt(window.prompt("input"));
   var res;
   function fab(n){
     if(n==1||n==2){
       return 1;
     }else{
       res = fab(n-1) + fab(n-2);
       return res;
     }
   }
   console.log(fab(n));
   
   //如果要返回整个列表：
   var l = [1,1,];
   for (var i = 3; i <= n; i++){
   	l.push(fab(i));
   }
   console.log(l);
   //input==11 --> [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
   ```

   ```javascript
   //4. 456反向输出
   //5. 输出最大值，if判断即可
   ```

   ```javascript
   //6. 100以内的质数：除了1和自身，不能再被整除
   var l = [];
   for (var i = 2; i < 100; i++){
   	var count = 0;//为每一个数计数，被整除的次数，为0时，为质数
   	for (var j = 2; j < i; j++){
   		if(i%j==0){
   			count++;
   		}
   	}
   	if (count == 0){
   		l.push(i);
   	}
   }
   console.log(l);
   
   //6.1 降低复杂度的算法
   //把
   for (var j = 2; j < i; j++)
   //换成以下即可：
   for (var j = 2; j < Math.sqrt(i); j++)
   ```

2. typeof(): 以下返回结果是什么？

   ```javascript
   alert(typeof(a));
   alert(typeof(undefined));
   alert(typeof(NaN));
   alert(typeof(null));
   var a = “123abc”;
   alert(typeof(+a));
   alert(typeof(!!a));
   alert(typeof(a + “”));
   alert(1 == “1”);
   alert(NaN == NaN);
   alert(NaN == undefined);alert( “11” + 11);
   alert( 1 === “1”);
   alert(parseInt(“123abc”));
   typeof(typeof(a)); 
   var num = 123123.345789;alert(num.toFixed(3));
   ```

   答案：

   ```javascript
   alert(typeof(a));         //undefined
   alert(typeof(undefined)); //undefiend
   alert(typeof(NaN));       //number
   alert(typeof(null));      //object
   var a = “123abc”;
   alert(typeof(+a));        //NaN
   alert(typeof(!!a));       //boolean
   alert(typeof(a + “”));    //string
   alert(1 == “1”);          //true
   alert(NaN == NaN);        //false
   alert(NaN == undefined);  //false, NaN不等于任何，包括自己。undefined == null，很神奇
   alert( “11” + 11);        //1111
   alert( 1 === “1”);        //false
   alert(parseInt(“123abc”));//123
   typeof(typeof(a));        //string
   var num = 123123.345789;
   alert(num.toFixed(3));    //123123.346
   ```

2. 写函数：

   1. 写一个函数，功能是告知你所选定的小动物的叫声。

   2. 写一个函数，实现加法计数器。 
   3. 定义一组函数，输入数字，逆转并输出汉字形式。 
   4. 写一个函数，实现 n 的阶乘。 
   5. 写一个函数，实现斐波那契数列。

   ```javascript
   //2. 加法
   var count = 0;
   function add(){
     ++count;
     console.log(count);
     return count;
   }
   
   add();add();add();add();add();add();
   //1 2 3 4 5 6 --> 一共调用了6次add()
   ```

   ```javascript
   //3. 
   //4. 阶乘递归，写过了。
   //5. 斐波那契数列递归，写过了。
   
   
   ```

   递归：1. 找规律；2. 找出口（停止的点）；

   优点：简洁；缺点：慢。

3. 算一个字符串的字节，利用

   ```javascript
   //str.charCodeAt(index)
   var i = window.prompt("input:");
   
   function total(n){
       var bytes = 0;
       for (i in n){
           var b = n.charCodeAt(i);
           if (b <= 255){
             bytes += 1;
           }else{
             bytes += 2;
           }
       }
       return bytes;
   }
   console.log(total(i));
   ```

   