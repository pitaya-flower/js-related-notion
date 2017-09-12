# js-related-notion
js相关概念
# JavaScript 定义了几种数据类型？ 哪些是原始类型？哪些是复杂类型？

```
最新的 ECMAScript 标准定义了 7 种数据类型:

原始类型

Number；数值类型；值：整数和小数。
String；字符串类型；值：字符串组成的文本。
Boolean；布尔类型；值：true、false。
Undefined；值：undefined（表示“未定义”或不存在，即由于目前没有定义）。
Null；值null（表示无值，即此处的值就是“无”的状态）。
Symbol；值：symbol（ECMAScript 6 新定义，表示唯一值）。

复杂类型
Object；对象类型；值：各种 “ key：value ” 组成的集合。

区别

原始类型（基本类型）都是存放着一个确定的值，它们对内存的占用大小是确定的，存放着栈内存中。
复杂类型存放的内容是不确定的，占用的内存也是变化的，它的栈内存用固定的内存存放它在内存中的位置，而可变化的内容存放着堆内存中。
基本类型变量存的是值，复杂类型的变量存的是内存地址。
基本类型在赋值的时候拷贝值，复杂类型在赋值的时候只拷贝地址，不拷贝值。
```
# 判断一个变量是否是数字、字符串、布尔、函数
```
JavaScript有三种方法，可以确定一个值到底是什么类型。

typeof运算符
instanceof运算符
Object.prototype.toString方法（以后再做介绍）

typeof 是用于返回一个值的数据类型，对于常见的几大数据类型都可以用typeof 数据类型的方式进行判断。

一元运算符，运算格式：
typeof xxx
返回结果是类型的字符串

数值、字符串、布尔值分别返回number、string、boolean。
typeof 123;      //number
typeof '123';    //string
typeof false;    //boolean

函数返回function。
function f() {};
typeof f;          //function
undefined返回undefined。
typeof undefined;   //undefined

除此以外，其他情况都返回object。（局限性）
typeof window;     //object
typeof {};        //object
typeof [];         //object
typeof null;     //object

instanceof 是用于判断某个对象是不是构造函数的一个实例，举例来说就是一个新声明的变量是不是调用了构造函数的内置属性或方法，区分狭义对象、数组、日期、函数等。

二元运算符
instanceof 是一个二元运算符，左边a是被运算的值，右边b是运算的类型。格式如下：
a instanceof b
使用instanceof的都必须是对象。所以不属于object类型的基本类型是无法应用instanceof的，或者无法得到你想要的结果。
1 instanceof Number
//false
new Number(1) instanceof Number
//true
'string' instanceof String
//false
new String('string') instanceof String
//true
返回结果是布尔值(Boolean):true/false
所以instanceof是一个判断，而typeof是求值
var o = {};
var a = [];
o instanceof Array;     //false
a instanceof Array;     //true
```
# NaN是什么? 有什么特别之处?
```
NaN 是一种特殊的 Number 类型值。
通常作为没有得到预期数值的返回值，如作为 Math 的某个方法的返回值出现的（例如：Math.sqrt(-1)）或者尝试将一个字符串解析成数字但失败了的时候（例如：parseInt("blabla")）
NaN是JavaScript之中唯一不等于自身的值。
typeof NaN   // "number"
NaN !== NaN  // true
 NaN === NaN  // false
任何涉及NaN的数值操作都会返回NaN，如NaN+10返回NaN
```
# 如何把非数值转化为数值?
```
在JavaScript中，有3个函数可以把非数值转换为数值，这三个函数分别是：Number() 、parselnt() 和 parseFloat()。

第一个函数，即转型函数 Nurnber() 可以用于任何数据类型，而另两个函数则专门用于把字符串转换成数值。这3个函数对于同样的输入会返回不同的结果。

Number() 函数

如果是 Boolean 值，true 和 false 将分别被转换为 1 和0；
如果是数字值，只是简单的传入和返回；
如来是null 值，返回 0；
如果是 undefined，返回NaN ；
如果是字符串，遵循下列规则：
如果字符串中只包含数字，则将其转换为十进制数值，即"1"会变成1 ， "123"会变成123，而"011"会变成11（注意，前导的0被忽略了）；
如果字符串中包含有效的浮点格式， 如"1.1"，则将其转换为对应的浮点数值（同样，也会忽略前导零）；
如果字符串中包含有效的十六进制格式，例如"0xf"，则将其转换为相同大小的十进制整数值；
如果字符串是空的（包含空字符） ，则将其转换为0；
如果字符串中包含除上述格式之外的字符，则将其转换为 NaN。

如果是对象，则调用对象的 valueOf() 方法，然后依照前面的规则转换返回的值。如果转换的结果是 NaN，则调用对象的 toString() 方法，然后再次依照前面的规则转换返回的字符串值。
var num1 = Number("Hello world!");  // NaN
var num2 = Number("   ");  // 0
var num3 = Numberl("000011");  // 11
var num4 = Number(true);  // 1

parseInt() 函数

由于 Number() 函数在转换字符串时比较复杂而且不够合理，因此在处理整数的时候更常用的是 parseInt() 函数。
parselnt() 函数在转换字符串时，更多的是看其是否符合数值模式，它会忽略字符串前面的空格，直至找到第一个非空格字符；如果第一个字符不是数字字符或者负号，parseInt() 就会返回 NaN；也就是说，用parselnt() 转换空字符时会返回 NaN（Nurnber() 对空字符返回 0）； 如果第一个字符是数字字符，parselnt() 会继续解析第二个字符，直到解析完所有后续字符或者遇到了一个非数字字符。例如，"1234blue"会被转换为1234 ，因为"blue"会被完全忽略；类似地，"'22.5"会被转换为22 ，因为小数点并不是有效的数字字符。
如果字符串中的第一个字符是数字字符，parselnt() 也能够识别出各种整数格式（即前面讨论的十进制、八进制和十六进制数) 。也就是说，如果字符以"0x"开头且后跟数字字符，就会将其当作一个十六进制整数；如果字符串以"0"开头且后跟数字字符，则会将其当作一个八迸制数来解析。
ES5不再允许将带有前缀0的数字视为八进制数，而是要求忽略这个0。但是，为了保证兼容性，大部分浏览器并没有部署这一条规定。
var num1 = parselnt ("1234blue") ;  // 1234
var num2 = parselnt (" ") ;   // NaN
var num3 = parselnt ("0xA") ;  // 10（十六进制数）
var num4 = parseInt(22.5);   // 22
var num5 = parselnt ("070") ;  // 56（八进制数）
var num6 = parselnt("70");  //70（十进制数）
var num7 = parselnt ("0xf") ;  // 15（十六进制数）
如果知道被解析的是十六进制格式的字符串，那么指定基数16 作为第二个参数，可以保证得到正确的结果，例如：
var num = parselnt("0xAF", 16);   //175
实际上，如果指定了16 作为第二个参数，字符串可以不带前面的"0x"，如下所示：
var num1 = parseInt( 'AF' , 16);   //175
var num2 = parselnt ("AF") ;   // NaN
指定基数会影响到转换的输出结果。例如：
var num1 = parselnt ("10", 2);  // 2（按照二进制解析）
var num2 = parseInt("10", 8);  // 8（按照八进制解析）
var num3 = parselnt("10", 10);  // 10（按照十进制解析）
var num4 = parselnt("10", 16);  // 16（按照十六进制解析）

parseFloat() 函数

与 parseInt () 函数类似，parseFloat () 也是从第一个字符（位置0）开始解析每个字符。而且也是一直解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止。也就是说，字符串中的第一个小数点是有效的，而第二个小数点就是无效的了，因此它后面的字符串将被忽略。举例来说，"22.34.5"将会被转换为22.34 。
除了第一个小数点有效之外， parseFloat () 与 parselnt() 的第二个区别在于它始终都会忽略前导的零。parseFloat() 可以识别前面讨论过的所有浮点数值格式，也包括十迸制整数格式，但十六进制格式的字符串则始终会被转换成0。由于 parseFloat() 只解析十进制值，因此它没有用第二个参数指定基数的用法。最后还要注意一点：如果字符串包含的是一个可解析为整数的数（没有小数点，或者小数点后都是零），parseFloat() 会返回整数。以下是使用 parseFloat() 转换数值的几个典型示例：
var num1 = parseFloat ("1234blue") ;  // 1234（整数）
var num2 = parseFloat("0xA");   // 0
var num3 = parseFloat("22.5");  // 22.5
var num4 = parseFloat("22.34.5");  // 22.5
var num5 = parseFloat("0908.5");   // 908
var num6 = parseFloat("3.125e7");   // 31250000
```

# ==与===有什么区别？
```
x == y 在对比 x 和 y 的值之前，会尝试对 x 和 y 做类型转换，变成同一种类型后，再对比。
x===y会对比x和y是否同类型，不同类型会返回false，不会发生转换。
== 会做类型转换，=== 不做类型转化
```
# break与continue有什么区别
```
二者都是为了控制代码循环执行，执行到之后都会立即跳出循环
break退出循环后，会继续执行后续的语句
for(var i=0;i<3;i++){
  for(var j=0;j<3;j++){
    console.log(j)
    break
  }
  console.log('我')
}
//0
//'我'
//0
//'我'
//0
//'我'
continue退出循环后，会再从最外层循环开始执行（注意外层循环次数没有累加）
for(var i=0;i<2;i++){
  for(var j=0;j<3;j++){
    console.log(j)
    continue
  }
  console.log('我')
}
//0
//1
//2
//"我"
//0
//1
//2
//"我"
```
# void 0 和 undefined在使用场景上有什么区别
```
undefined 全局作用域下不能被重写，但是在局部作用域中，可以被重写的。所以undefined现常用于全局环境。
void 运算符通常只用于获取 undefined 的原始值，一般使用 void(0)（等同于 void 0）。在上述情况中，也可以使用全局变量undefined 来代替（假定其仍是默认值）。
而 void 可以给任何给定的表达式求值，并返回 undefined,并且 void 不可被重写，因此void 0是在局部作用域中替代undefined的最佳选择 。
```
# 以下代码的输出结果及原因
 ```
console.log(1+1);
console.log(1+1);　　　　　 // 2
"+" 两边都是数值类型，做数值运算。
```
```
console.log("2"+"4");
console.log("2"+"4");　　　　//24
"+" 两边都是字符串类型，直接拼接。
```
```
console.log(2+"4");
console.log(2+"4");　　　　//24
"+" 一边是数值类型，另一边是字符串类型，数值类型转为字符串类型后拼接。
```
```
console.log(+"4");
console.log(+"4");　　　　//4
"+" 只有右侧一个操作数，转换我数值类型。
```
# 以下代码的输出结果及原因
```
var a = 1;
a+++a;
typeof a+2;
var a = 1;　　　　　　　
console.log(a+++a);　　　　　//3
console.log(typeof a+2);　　　　　//number2
因为"…++"优先级高于"+"优先级高于"++…"，"a+++a" 相当于"(a++)+a"，即"1+2"返回 3 ；
"typeof a+2"相当于"(typeof a)+2"，即"number+2"，做字符串拼接返回number2。
```
# 以下代码的输出结果及原因
```
 var a = 1;
 var b = 3;
 console.log( a+++b );　　　//4
因为"…++"优先级高于"+"优先级高于"++…"，"a+++b" 相当于"(a++)+b"，即"1+3"返回 4；
```

# 遍历数组，把数组里的打印数组每一项的平方
```
 var arr=[3,4,5]
for(var i in arr){
  console.log(arr[i]*arr[i])
}
//9
//16
//25
```
# 遍历 JSON, 打印里面的值
```
var obj = {
 name: 'hunger', 
 sex: 'male', 
 age: 28 
}
for(var key in obj){
  console.log(key+':'+obj[key])
}
//"name:hunger"
//"sex:male"
//"age:28"
```
#  以下代码输出结果及原因
```
var a = 1, b = 2, c = 3;
var val = typeof a + b || c >0
console.log(val) 
//"number2"
优先级：typeof>"+">"||"，所以相当于"number2" || c>0，返回"number2"。
```
```
var d = 5;
var data = d ==5 && console.log('bb')
console.log(data)
//"bb"
//undefined
优先级："==">"+"&&"，所以相当于true && undefined，返回undefined。
```
```
var data2 = d = 0 || console.log('haha')
console.log(data2)
//"haha"
//undefined
相当于data2=d=0|| undefined，0布尔值为false，所以返回undefined。
```
```
var x = !!"Hello" + (!"world", !!"from here!!");
console.log(x)
//2
优先级："=">"!">"+"，相当于var x=true + (false,true)，加号优先将操作数转为数字，所以得到2。
```
