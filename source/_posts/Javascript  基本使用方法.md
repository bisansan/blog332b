---
title: Javascript  基本使用方法
tags: []
id: '551'
categories:
  - - JavaScript
abbrlink: '46115975'
date: 2019-02-04 12:11:47
---

**javascript引入的常见三种方式** 1.行内使用 `<input type="button" name="button" value="点击" onclick="window.alert('嘻嘻')">`   2.内部使用

 <input type="button" name="aaa" value="点击" onclick="myfunc()">
<script type="text/javascript">
function myfunc()
{
window.alert('弹出框');
};
</script>

  三.外部引入

<script src="js/test.js"></script>

  常用的一下几种方式引入js代码：

1.  在页面中直接写入<script type="text/javascript">js代码</script>。
2.  在页面中引入外部文件<script src="xx.js"></script>。
3.  在js中引入外部js，通过document.wirite("scr"+"ipt src='xx.js'></scr"+"ipt">。
4.  在js中引用其他js片段，document.write("<scr"+"ipt>alert(xxx)</scr"+"ipt>")。
5.  通过DOM添加：var scr=document.createElement("script"); scr.src="xxx.js";

  **javascript输出的四种方式** 一、window.alert()       弹出一个对话框 `window.alert('我是对话框')`   二、innerHTML       操作html里面的元素 `<p id='demo'>我是一个段落</p>` `<script>` `document.getElementById("demo").innerHTML = "修改这个段落";` `window.alert(document.getElementById("demo").innerHTML);` `//获取这个元素里面的值` `</script>`   三、document.write()  直接输出内容 `<script>document.write('我是文字')</script>` _如果在文档已完成加载后执行 document.write，整个 HTML 页面将被覆盖。_   四、console.log()  输出到控制台 chrome浏览器中使用 F12 来启用调试模式， 在调试窗口中点击 "Console" 菜单，输入的内容会出现在哪里 `<script>console.log('我是文字，请在控制台查看我');</script>`    

1.当编写 JavaScript 语句时，请留意是否关闭大小写切换键。 函数 **getElementById** 与 **getElementbyID** 是不同的。 同样，变量 **myVariable** 与 **MyVariable** 也是不同的。   2. 单行注释”//“，多行注释以”/\*“开始，用”\*/“来注释   3.关键字

语句

描述

break

用于跳出循环。

catch

语句块，在 try 语句块执行出错时执行 catch 语句块。

continue

跳过循环中的一个迭代。

do ... while

执行一个语句块，在条件语句为 true 时继续执行该语句块。

for

在条件语句为 true 时，可以将代码块执行指定的次数。

for ... in

用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）。

function

定义一个函数

if ... else

用于基于不同的条件来执行不同的动作。

return

退出函数

switch

用于基于不同的条件来执行不同的动作。

throw

抛出（生成）错误 。

try

实现错误处理，与 catch 一同使用。

var

声明一个变量。

while

当条件语句为 true 时，执行语句块。

  4.声明变量用var，例如：`var beare = 'good';`，声明多个变量的方法：`var beare = 'good',beis = 'bad';` _注意不能这样定义多个变量为一个值，这样定义只有benot=1，其他为空值_ `var beare,beis,benot=1;`   5.数据类型 数据类型变量声明办法 var carname=new String;       ##字符串 var x=      new Number;     ##数字类型 var y=      new Boolean;     ##布尔类型 var cars=   new Array;      ##数组类型 var person= new Object;      ##对象类型（类似字典） 代码演示：`var you123 = new String('我是字符串');` 对象的值可以通过关键key和属性来访问，假如有代码如下 `var person= { firstname : "John", lastname : "Doe", id : 5566 };` `person.firstname`和`person['firstname']`都可以得到“John”这个值 如果函数作为属性存入对象里面，它有一个属性this就是代表这个对象本身，这个是方便再对象自身中引用 假如一个值重新声明变量，它的值是不会改变的，除非再给它重新赋值 如果你在声明变量的时候没有使用var，那么这个变量就会成为window的一个属性，

bbc =  '我是字符串';     //没有使用var可以配置全局属性

document.write(this.bbc);   //获取上面的的字符串

document.write(window.bbc);   //效果一样，等同上面

delete bbc; //无法删除，只能删除var声明的变量

1.通过`var str123 = new String('字符串');` 中的new来声明，是一个对象，而不是一个字符串，和`var str123 = '字符串';` 不相等 2.’===‘代表数据和类型绝对相等，string.length可以返回字符串的长度   onload 和  onpageshow  区别 onload : 在元素载入完成后执行的代码，载入缓存不执行 onpageshow：每次载入图片元素后执行的代码，载入缓存依旧会执行 支持onload的标签：<body>, <frame>, <frameset>, <iframe>, <img>, <input type="image">, <link>, <script>, <style> 例如我们在img标签中使用onload标签，就可以判断图片是否载入

<script>
      var loadimage = document.getElementById('loadimageid');
      var loadimageerror = "alert('载入错误')";
      // loadimage.onload="alert('图片载入成功')";
      loadimage.onpageshow=alert('载入图片成功');
</script>

  if...else if...else  判断语句 if：条件一   else if：条件二    else：都不满足，就执行这里 and：符号&&   多个条件拼接 ，必须满足所有条件 or：符号      多个条件拼接，满足其中一个就行了 not：符号!     条件相关的结果

<script>
    var a = 3;
    if (a != 3) {
        window.alert('条件一')
    }
    else if (a = 3) {
        window.alert('条件二')
    }
    else {
        window.alert('都不满足，就执行else')
    }
</script>

  switch...case...default switch是基于不同条件执行不同命令，switch中通常是一个变量，如果满足case就执行case的命令，（）用break隔开，防止满足一次条件，就执后面所有代码）如果不满足就继续向下寻找，如果没找到就默认执行default

<script>
    var a = 9;
    switch (a) {
        case 1:alert('1');
        break;
        case 2:alert('2');
        break;
        default:alert('默认值');
    }
</script>

  for 循环执行某一块的代码 for (a;b;c) { 需要被循环执行的代码 } a 循环执行前执行的代码 b 决定循环执行的条件 c 每次循环执行后执行的代码 实例代码

<script>
    for (var a=1;a<5;a++) {
        document.write('数字'+a+'<br>');
    };
</script>

  for....in 循环 循环一个数组

<script>
    var a = \['a','b','c'\];
    for (var b in a) {
        window.alert(b+'：'+a\[0\]);
    };
</script>

循环一个对象

<script>
    var a = {a1:'a',a2:'b',a3:'c'};
    for (var b in a) {
        window.alert(b+'：'+a\[b\]);
    };
</script>

  while循环

<script>
    var a = 1;
    while (a<5 && a>0) {
        a++;
        window.alert(a);
    }
</script>

  Break 和 Continue 语句 Break：跳出整个循环（可以在switch和循环中使用） Continue：跳出当前循环，去执行下一个循环（只能在循环中使用）   javascript标签 label: statements 通过标签引用，break 语句可用于跳出任何 JavaScript 代码块   NaN和isNaN 判断这个值是不是数字 详细说明：[http://www.w3school.com.cn/jsref/jsref\_nan\_number.asp](http://www.w3school.com.cn/jsref/jsref_nan_number.asp)   在 JavaScript 中有 5 种不同的数据类型： string number boolean object function 3 种对象类型： Object Date Array 2 个不包含任何值的数据类型： null undefined 判断是不是字符串的方法

<script>
    var a = 'aaa';
    if (typeof(a) == 'string') {
        document.write('他是字符串');
    }
    else{
        document.write('他不是字符串');
    };
</script>

  查询对应的构造函数key.constructor "John".constructor   //function String() { \[native code\] } 根据它来判断对应的对象类型   数据转换 字符串转换：全局方法String()和value.toString() 1.toString可以将所有类型转换成字符串，但不包括null和undefined 2.String可以将null和undefined转换为字符串，但是没法转进制字符串，例如二进制，八进制，十六进值 String(value);或者value.toString()

1.  toExponential() 把对象的值转换为指数计数法。
2.  toFixed() 把数字转换为字符串，结果的小数点后有指定位数的数字。
3.  toPrecision() 把数字格式化为指定的长度。

  数字转换：Number() 空字符串会转换成0，如果不是字符串就会转换成NaN Number(value);

1.  parseFloat() 解析一个字符串，并返回一个浮点数。
2.  parseInt() 解析一个字符串，并返回一个整数。

  一元运算符 + Operator + 可用于将变量转换为数字： 实例 var y = "5"; // y 是一个字符串 var x = + y; // x 是一个数字   将布尔值转换为数字 全局方法 Number() 可将布尔值转换为数字。 Number(false) // 返回 0 Number(true) // 返回 1   布尔类型：Boolean()   javascript正则表达式 var patt = /runoob/i 加i代表不区分大小写   javascript错误 1.try 和 catch是用来处理 try 语句测试代码块的错误。 catch 语句处理错误。 如果try中没有任何错误，就不会执行catch里面的语句   2.throw  自定义错误 如果把 throw 与 try 和 catch 一起使用，那么您能够控制程序流，并生成自定义的错误消息。下面是验证输入的数字 注意：input输入值是字符串，需要用Number格式化成数字

<p>不管输入是否正确，输入框都会再输入后清空。</p>
<p>请输入 5 ~ 10 之间的数字：</p>

<input id="demo" type="text">
<button type="button" onclick="myFunction()">点我</button>

<p id="p01"></p>

<script>
    function myFunction() {
        var message, x;
        message = document.getElementById("p01");
        message.innerHTML = "";
        x = document.getElementById("demo").value;
        try {
            if(x == "") throw "值是空的";
            if(isNaN(x)) throw "值不是一个数字";
            x = Number(x);   //input输入值是字符串，用Number格式化成数字
            if(x > 10) throw "太大";
            if(x < 5) throw "太小";
        }
        catch(err) {
            message.innerHTML = "错误: " + err + ".";
        }
        finally {
            document.getElementById("demo").value = "";
        }
    }
</script>

  3.finally 语句 finally 语句不论之前的 try 和 catch 中是否产生异常都会执行该代码块。 try { ... //异常的抛出 } catch(e) { ... //异常的捕获与处理 } finally { ... //结束处理 }   JS验证表单

<script>
    function fa() {
        return false;   //返回false阻止表单提交
    }
</script>
<form action="#" onsubmit="return fa()">      <!--用return阻止提交-->
    <input type="text">
    <input type="submit">
</form>

js获取表单值 [http://www.runoob.com/js/js-form-validation.html](http://www.runoob.com/js/js-form-validation.html)   javascript Json JSON.parse() 用于将一个 JSON 字符串转换为 JavaScript 对象。 JSON.stringify() 用于将 JavaScript 值转换为 JSON 字符串。

<script>
    var asy = \['ad','ac','aqw'\];
    var obj = JSON.stringify(asy);
    document.write(obj)
</script>

  javascript  查找最大的数

<script>
    var ti=\[123,45,73,1048\];
    var i=0,x=ti\[0\];
    for (;ti.length > i;i++) {
        if (x < ti\[i\]){
            x = ti\[i\]
        }
    }
    alert(x)
</script>

  1.在一个函数里面使用this代表整个window对象，除非你在里面嵌套一个函数，这样你在嵌套里面使用this就代表外面包括的这个函数本身 2.函数可以这样调用window.function()   DOM javascript查找html方式 1.javascript 通过tag标签来查找元素，tag来查找元素，他会将这个页面的所有该元素的东西放入一个array数组里面去

<body>
<p>111111</p>
<button onclick="x()">点击</button>
<script>
    function x (){
        x = window.document.getElementsByTagName('p')
        alert(x\[0\].innerHTML)
    }
</script>
</body>

  2.通过id来查找元素 var x=document.getElementById("intro");   3.通过类名来查找 var x=document.getElementsByClassName("intro");   4.修改html的属性

<a href="http://www.baidu.com" id="po">百度</a>
<button onclick="x()">点击</button>
<script>
    function x (){
        x = window.document.getElementById('po')
        alert(x.href)
    }
</script>

  5.通过javascript修改css样式

<a href="http://www.baidu.com" id="po">百度</a>
<script>
        window.document.getElementById('po').style.color = 'red';
</script>

6.HTML DOM EventListener  监听事务

_element_.addEventListener(_event, function, useCapture_);

第一个参数是事件的类型 (如 "click" 或 "mousedown"). 第二个参数是事件触发后调用的函数。 第三个参数是个布尔值用于描述事件是冒泡还是捕获。该参数是可选的。 addEventListener() 方法允许向同一个元素添加多个事件，且不会覆盖已存在的事件：

<script>
x = document.getElementById("myBtn");
x.addEventListener("click", function(){alert("Hello World!");});
</script>

冒泡事件和事务事件 [https://www.cnblogs.com/christineqing/p/7607113.html](https://www.cnblogs.com/christineqing/p/7607113.html)   7.添加和删除、替换html元素 appendChild() 添加元素，添加在末尾

<div id="div1">
</div>
<script>
    var p1 = document.createElement("p");  //创建p元素
    var text = document.createTextNode('这是一段文本！');  //创建文本元素
    p1.appendChild(text);    //将文本元素添加p元素里
    var div1 = document.getElementById('div1');
    div1.appendChild(p1);     //将p1元素添加到div1当中
</script>

  insertBefore()  添加元素，插入指定元素前面

<div id="div1">
    <p id="p2">这是第二段文本，没有js它就是第一行</p>
</div>
<script>
    var p1 = document.createElement("p");  //创建p元素
    var text = document.createTextNode('这是一段文本！');  //创建文本元素
    p1.appendChild(text);    //将文本元素添加p元素里
    var div1 = document.getElementById('div1');
    var p2 = document.getElementById('p2');
    div1.insertBefore(p1,p2)
</script>

  removeChild() 移除已存在的元素

<div id="div1">
    <p id="p1">这是一段文本！</p>
    <p id="p2">这是第二段文本！</p>
</div>
<script>
    var div1 = document.getElementById('div1');
    var p2 = document.getElementById('p2');
    div1.removeChild(p2);
</script>

  replaceChild()  替换 HTML 元素

<div id="div1">
    <p id="p1">这是一段文本！</p>
    <p id="p2">这是第二段文本！</p>
</div>
<script>
    var pdemo = document.createElement("p");  //创建p元素
    var text = document.createTextNode('这是一段特殊文本！');  //创建文本元素
    pdemo.appendChild(text);    //将文本元素添加p元素里
    var div1 = document.getElementById('div1');
    var p2 = document.getElementById('p2');
    div1.replaceChild(pdemo,p2)
</script>

  javascript高级对象 1.遍历一个对象

<div id="div1">
    <p id="p1">这是一段文本！</p>
    <p id="p2">这是第二段文本！</p>
</div>
<button onclick="f()">点击</button>
<script>
    var p2 = document.getElementById('p2');
    var k1 = {
      k1:'我是苹果',
      k2:'我是香蕉',
      k3:'我是栗子'
    };
    function f() {
        for (x in k1) {
            p2.innerHTML +=x+'：'+k1\[x\]+"<br>";
        }
    }
</script>

  2.创建一个对象的三种方式 [https://www.cnblogs.com/dongjc/p/5179561.html](https://www.cnblogs.com/dongjc/p/5179561.html)   字符串转为数组

<p id="demo">单击按钮显示数组。</p>
<button onclick="myFunction()">点我</button>
<script>
    function myFunction(){
        var str="a,b,c,d,e,f";
        var n=str.split(",");
        document.getElementById("demo").innerHTML=n\[0\];
    }
</script>

  给变量设置时间（可用于对当前时间做比较）

<p id="demo">单击按钮显示修改后的年月日。</p>
<button onclick="myFunction()">点我</button>
<script>
    function myFunction(){
        var d = new Date();
        d.setFullYear(2020,10,3);
        var x = document.getElementById("demo");
        x.innerHTML=d;
    }
</script>
<p>记住 JavaScript 月数是从0至11。10是11月。</p>

  数组对象 合并一个数组或者多个 array1.concat(array2, array3);   如果布尔对象无初始值或者其值为:

1.  0
2.  \-0
3.  null
4.  ""
5.  false
6.  undefined
7.  NaN

  window.location.assign和window.location.replace(url) 区别 window.location.assign(url) ： 加载 URL 指定的新的 HTML 文档。 就相当于一个链接，跳转到指定的url，当前页面会转为新页面内容，可以点击后退返回上一个页面。 window.location.replace(url) ： 通过加载 URL 指定的文档来替换当前文档 ，这个方法是替换当前窗口页面，前后两个页面共用一个   三种弹框 警告框 window.alert("_sometext_");   确认框 当你点击 "确认", 确认框返回 true， 如果点击 "取消", 确认框返回 false。 window.confirm("_sometext_");   提示框 提示用户输入某个值，可以指定默认值 window.prompt("_sometext_","_defaultvalue_");   计时执行 不间断间隔执行 setInterval() 间隔指定的毫秒数不停地执行指定的代码 window.setInterval("_javascript function_",_milliseconds_);   停止制作 clearInterval() window.clearInterval(_intervalVariable_)   指定时间执行    setTimeout() window.setTimeout("_javascript function_", _milliseconds_);   停止执行 setTimeout() window.setTimeout("_javascript function_", _milliseconds_);