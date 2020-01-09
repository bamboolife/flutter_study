# Dart语言学习
## 语言特性
- Dart所有的东西都是对象， 即使是数字numbers、函数function、null也都是对象，所有的对象都继承自Object类。

- Dart动态类型语言, 尽量给变量定义一个类型，会更安全，没有显示定义类型的变量在 debug 模式下会类型会是 dynamic(动态的)。

- Dart 在 running 之前解析你的所有代码，指定数据类型和编译时的常量，可以提高运行速度。

- Dart中的类和接口是统一的，类即接口，你可以继承一个类，也可以实现一个类（接口），自然也包含了良好的面向对象和并发编程的支持。

- Dart 提供了顶级函数(如：main())。

- Dart 没有 public、private、protected 这些关键字，变量名以"_"开头意味着对它的 lib 是私有的。

- 没有初始化的变量都会被赋予默认值 null。

- final的值只能被设定一次。const 是一个编译时的常量，可以通过 const 来创建常量值，var c=const[];，这里 c 还是一个变量，只是被赋值了一个常量值，它还是可以赋其它值。实例变量可以是 final，但不能是 const。

- 编程语言并不是孤立存在的，Dart也是这样，他由语言规范、虚拟机、类库和工具等组成：
  - SDK：SDK 包含 Dart VM、dart2js、Pub、库和工具。
  - Dartium：内嵌 Dart VM 的 Chromium ，可以在浏览器中直接执行 dart 代码。
  - Dart2js：将 Dart 代码编译为 JavaScript 的工具。
  - Dart Editor：基于 Eclipse 的全功能 IDE，并包含以上所有工具。支持代码补全、代码导航、快速修正、重构、调试等功能。
## 关键字
| 关键字 |      |     |      |
|:------:|:-----|:-----:|:------:|
| abstract	| do	| import	| super |
| as	| dynamic	| in	| switch |
| assert	| else	| interface	| sync* |
| enum	| implements | 	is	| this |
| async*	| export	| library	| throw |
| await	| external	| mixin	| true |
| break	| extends	| new	| try |
| case	| factory	| null	| typedef |
| catch	| false	| operator	| var |
| class	| final	| part	| void |
| const	| finally	| rethrow	| while |
| continue	| for	| return	| with |
| covariant| 	get	| set	| yield* |
| default	| if	| static	| deferred |

## 变量与常量

### 1.变量声明与初始化

调用的变量name包含对String值为“张三” 的对象的引用，name推断变量的类型是String，但可以通过指定它来更改该类型，如果对象不限于单一类型（没有明确的类型），请使用Object或dynamic关键字。
```dart
// 没有明确类型，编译的时候根据值明确类型
  var name = ‘Bob’; 
  Object name = '张三';
  dynamic name = '李四';

  // 显示声明将被推断类型, 可以使用String显示声明字符串类型
  String name = 'Bob' ;
```
### 2.默认值

未初始化的变量的初始值为null（包括数字），因此数字、字符串都可以调用各种方法

```dart
//测试 数字类型的初始值是什么?
  int lineCount;
  // 为false的时候抛出异常
  assert(lineCount == null);
  print(lineCount); //打印结果为null，证明数字类型初始化值是null
```

### 3.final and const
- 如果您从未打算更改一个变量，那么使用 final 或 const，不是var，也不是一个类型。
一个 final 变量只能被初始化一次; const变量是一个编译时常量，(Const变量是隐式的final)
final的顶级或类变量在第一次使用时被初始化。
- 被final修饰的顶级变量或类变量在第一次声明的时候就需要初始化。
```dart
// The final variable 'outSideFinalName' must be initialized.
final String outSideFinalName
```
- 被final或者const修饰的变量，变量类型可以省略，建议指定数据类型。

```dart
//可以省略String这个类型声明
 final name = "Bob";
 final String name1  = "张三";
 
 const name2 = "alex";
 const String name3 = "李四";

```
- 被 final 或 const 修饰的变量无法再去修改其值。

```dart
final String outSideFinalName = "Alex";
 // outSideFinalName', a final variable, can only be set once
 // 一个final变量，只能被设置一次。
 outSideFinalName = "Bill";
 
 const String outSideName = 'Bill';
 // 这样写，编译器提示：Constant variables can't be assigned a value
 // const常量不能赋值
 // outSideName = "小白";
```
- flnal 或者 const 不能和 var 同时使用

```dart
// Members can't be declared to be both 'const' and 'var'
 const var String outSideName = 'Bill';
 
 // Members can't be declared to be both 'final' and 'var'
 final var String name = 'Lili';

```
- 常量如果是类级别的，请使用 static const
```dart
// 常量如果是类级别的，请使用 static const
 static const String name3 = 'Tom';
 
 // 这样写保存
 // Only static fields can be declared as const
 // 只有静态字段可以声明为const
 //const String name3 = 'Tom';
```
- 常量的运算
```dart
 const speed = 100; //速度（km/h）
 const double distance = 2.5 * speed; // 距离 = 时间 * 速度

 final speed2 = 100; //速度（km/h）
 final double distance2 = 2.5 * speed2; // 距离 = 时间 * 速度
```
- const关键字不只是声明常数变量，您也可以使用它来创建常量值，以及声明创建常量值的构造函数，任何变量都可以有一个常量值。

```dart
// 注意: [] 创建的是一个空的list集合
 // const []创建一个空的、不可变的列表（EIL）。
 var varList = const []; // varList 当前是一个EIL
 final finalList = const []; // finalList一直是EIL
 const constList = const []; // constList 是一个编译时常量的EIL

 // 可以更改非final,非const变量的值
 // 即使它曾经具有const值
 varList = ["haha"];

 // 不能更改final变量或const变量的值
 // 这样写，编译器提示：a final variable, can only be set once
 // finalList = ["haha"];
 // 这样写，编译器提示：Constant variables can't be assigned a value  
 // constList = ["haha"];
```
- 在常量表达式中，该运算符的操作数必须为'bool'、'num'、'String'或'null', const常量必须用conat类型的值初始化。
```dart
const String outSideName = 'Bill';
final String outSideFinalName = 'Alex';
const String outSideName2 = 'Tom';

const aConstList = const ['1', '2', '3'];

// In constant expressions, operands of this operator must be of type 'bool', 'num', 'String' or 'null'
// 在常量表达式中，该运算符的操作数必须为'bool'、'num'、'String'或'null'。
const validConstString = '$outSideName $outSideName2 $aConstList';

// Const variables must be initialized with a constant value
// const常量必须用conat类型的值初始化
const validConstString = '$outSideName $outSideName2 $outSideFinalName';

var outSideVarName='Cathy';
// Const variables must be initialized with a constant value.
// const常量必须用conat类型的值初始化
const validConstString = '$outSideName $outSideName2 $outSideVarName';

// 正确写法
const String outSideConstName = 'Joy';
const validConstString = '$outSideName $outSideName2 $outSideConstName';
```
## 数据类型
### 1.num
- num 是数字类型的父类，有两个子类 int 和 double。

- int 根据平台的不同，整数值不大于64位。在Dart VM上，值可以从-263到263 - 1，编译成JavaScript的Dart使用JavaScript代码，允许值从-253到253 - 1。

- double 64位（双精度）浮点数，如IEEE 754标准所规定。

```dart
int a = 1;
 print(a);
 
 double b = 1.12;
 print(b);
 
 // String -> int
 int one = int.parse('1');
 // 输出3
 print(one + 2);
 
 // String -> double
 var onePointOne = double.parse('1.1');
 // 输出3.1
 print(onePointOne + 2);

 // int -> String
 String oneAsString = 1.toString();
 // The argument type 'int' can't be assigned to the parameter type 'String'
 //print(oneAsString + 2);
 // 输出 1 + 2
 print('$oneAsString + 2');
 // 输出 1 2
 print('$oneAsString 2');

 // double -> String 注意括号中要有小数点位数，否则报错
 String piAsString = 3.14159.toStringAsFixed(2);
 // 截取两位小数, 输出3.14
 print(piAsString);
 
 String aString = 1.12618.toStringAsFixed(2);
 // 检查是否四舍五入，输出1.13，发现会做四舍五入
 print(aString);
```
### 2.String

- art里面的String是一系列 UTF-16 代码单元。
- 您可以使用单引号或双引号来创建一个字符串。
- 单引号或者双引号里面嵌套使用引号。
- 用 或{} 来计算字符串中变量的值，需要注意的是如果是表达式需要${表达式}

```dart
String singleString = 'abcdddd';
 String doubleString = "abcsdfafd";
 
 String sdString = '$singleString a "bcsd" ${singleString}';
 String dsString = "abc 'aaa' $sdString";
 print(sdString);
 print(dsString);


 String singleString = 'aaa';
 String doubleString = "bbb";
 // 单引号嵌套双引号
 String sdString = '$singleString a "bbb" ${doubleString}';
 // 输出 aaa a "bbb" bbb
 print(sdString);
 
 // 双引号嵌套单引号
 String dsString = "${singleString.toUpperCase()} abc 'aaa' $doubleString.toUpperCase()";
 // 输出 AAA abc 'aaa' bbb.toUpperCase(), 
 可以看出 ”$doubleString.toUpperCase()“ 没有加“{}“，导致输出结果是”bbb.toUpperCase()“
 print(dsString);
```
### 3.bool

- Dart 是强 bool 类型检查，只有bool 类型的值是true 才被认为是true。
- 只有两个对象具有bool类型：true和false，它们都是编译时常量。
- Dart的类型安全意味着您不能使用 if（nonbooleanValue） 或 assert（nonbooleanValue） 等代码, 相反Dart使用的是显式的检查值。
- assert 是语言内置的断言函数，仅在检查模式下有效
在开发过程中， 除非条件为真，否则会引发异常。(断言失败则程序立刻终止)。



