toString()方法可以根据所传递的参数把数值转换为对应进制的数字字符串。参数范围为 2~36 之间的任意整数。
    var a = 32;
    console.log(a.toString(2));  //返回字符串100000
    console.log(a.toString(4));  //返回字符串200
    console.log(a.toString(16));  //返回字符串20
    console.log(a.toString(30));  //返回字符串12
    console.log(a.toString(32));  //返回字符串10
1
2
3
4
5
6
数值直接量不能直接调用 toString() 方法，必须先使用小括号或其他方法转化数字。
    console.log(123.toString());  //抛出语法错误   相当于打印 123.0toString()
	console.log(1.23.toString());   //返回123
    console.log((123).toString());   //返回123
	console.log(123 .toString());   //返回123
	var a = 123;
	console.log(a.toString());   //返回123
1
2
3
4
5
6
注意
1.undefined和null没有toString()方法
2.布尔型数据true和false返回对应的’true’和’false’
3.字符串类型原值返回
4.数值类型的情况较复杂
4.1、正浮点数及NaN、Infinity加引号返回

1.23.toString();//'1.23'
NaN.toString();//'NaN'
Infinity.toString();//'Infinity'
1
2
3
4.2、负浮点数或加’+'号的正浮点数直接跟上.toString()，相当于先运行toString()方法，再添加正负号，转换为数字

+1.23.toString();//1.23
typeof +1.23.toString();//'number'
-1.23.toString();//-1.23
typeof -1.23.toString();//'number'
1
2
3
4
4.3、整数直接跟上.toString()形式，会报错，提示无效标记，因为整数后的点会被识别为小数点

0.toString();//Uncaught SyntaxError: Invalid or unexpected token
1
因此，为了避免以上无效及报错的情况，数字在使用toString()方法时，加括号可解决

(0).toString();//'0'
(-0).toString();//'0'
(+1.2).toString();//'1.2'
(-1.2).toString();//'-1.2'
(NaN).toString();//'NaN'
1
2
3
4
5
此外，数字类型的toString()方法可以接收表示转换基数(radix)的可选参数，如果不指定此参数，转换规则将是基于十进制。同样，也可以将数字转换为其他进制数(范围在2-36)

var n = 17;
n.toString();//'17'
n.toString(2);//'10001'
n.toString(8);//'21'
n.toString(10);//'17'
n.toString(12);//'15'
n.toString(16);//'11'
1
2
3
4
5
6
7
（5）对象Object类型及自定义对象类型加括号返回[object Object]

{}.toString();//报错，Unexpected token .
({}).toString();//[object Object]
({a:123}).toString();//[object Object]
Object.toString();//"function Object() { [native code] }"
1
2
3
4
function Person(){
    this.name = 'test';
}
var person1 = new Person();
person1.toString();//"[object Object]"
1
2
3
4
5
类型识别

常常使用Object.prototype.toString()来进行类型识别，返回代表该对象的[object 数据类型]字符串表示

[注意]Object.prototype.toString()可以识别标准类型及内置对象类型，但不能识别自定义类型

console.log(Object.prototype.toString.call("jerry"));//[object String]
console.log(Object.prototype.toString.call(12));//[object Number]
console.log(Object.prototype.toString.call(true));//[object Boolean]
console.log(Object.prototype.toString.call(undefined));//[object Undefined]
console.log(Object.prototype.toString.call(null));//[object Null]
console.log(Object.prototype.toString.call({name: "jerry"}));//[object Object]

console.log(Object.prototype.toString.call(function(){}));//[object Function]
console.log(Object.prototype.toString.call([]));//[object Array]
console.log(Object.prototype.toString.call(new Date));//[object Date]
console.log(Object.prototype.toString.call(/\d/));//[object RegExp]
function Person(){};
console.log(Object.prototype.toString.call(new Person));//[object Object]
1
2
3
4
5
6
7
8
9
10
11
12
13
function type(obj){
    return Object.prototype.toString.call(obj).slice(8,-1).toLowerCase();
}
console.log(type("jerry"));//"string"
console.log(type(12));//"number"
console.log(type(true));//"boolean"
console.log(type(undefined));//"undefined"
console.log(type(null));//"null"
console.log(type({name: "jerry"}));//"object"

console.log(type(function(){}));//"function"
console.log(type([]));//"array"
console.log(type(new Date));//"date"
console.log(type(/\d/));//"regexp"
function Person(){};
console.log(type(new Person));//"object"
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
其他识别

除了类型识别之外，还可以进行其他识别，如识别arguments或DOM元素

(function(){
    console.log(Object.prototype.toString.call(arguments));//[object Arguments]
})()
console.log(Object.prototype.toString.call(document));//[object HTMLDocument]
1
2
3
4
（6）函数Function类型返回函数代码

当我们对一个自定义函数调用toString()方法时，可以得到该函数的源代码；如果对内置函数使用toString()方法时，会得到一个’[native code]'字符串。因此，可以使用toString()方法来区分自定义函数和内置函数

function test(){
    alert(1);//test
}
test.toString();/*"function test(){
                    alert(1);//test
                  }"*/
Function.toString();//"function Function() { [native code] }"
1
2
3
4
5
6
7
（7）数组Array类型返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串

[].toString();//''
[1].toString();//'1'
[1,2,3,4].toString();//'1,2,3,4'
Array.toString();//"function Array() { [native code] }"
1
2
3
4
（8）时间Date类型返回表示当前时区的时间的字符串表示

(new Date()).toString();//"Sun Jun 05 2016 10:04:53 GMT+0800 (中国标准时间)"
Date.toString();//"function Date() { [native code] }"
1
2
（9）正则表达式RegExp类型返回正则表达式字面量的字符串表示

/ab/i.toString();//'/ab/i'
/mom( and dad( and baby)?)?/gi.toString();//'mom( and dad( and baby)?)?/gi'
RegExp.toString();//"function RegExp() { [native code] }"
1
2
3
（10）错误Error类型

Error.toString();//"function Error() { [native code] }"
RangeError.toString();//"function RangeError() { [native code] }"
ReferenceError.toString();//"function ReferenceError() { [native code] }"
SyntaxError.toString();//"function SyntaxError() { [native code] }"
TypeError.toString();//"function TypeError() { [native code] }"
URIError.toString();//"function URIError() { [native code] }"