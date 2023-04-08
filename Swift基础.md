# 一、命名规则

名称必须以字母或下划线开头，之后可以是任何字母、下划线或0～9之间的数字组合。Swift中是区分大小写的。

# 二、数据类型

## 1.基础数据类型

| 类型   | 大小                                                         | 区间值                                      | 说明                                             |
| ------ | ------------------------------------------------------------ | ------------------------------------------- | ------------------------------------------------ |
| Int    | 在32位平台上，`Int32`长度相同。在64位平台上，`Int64`长度相同。 |                                             | 有符号整数，长度与当前平台的原生字长相同。       |
| UInt   | 在32位平台上，UInt32`长度相同。在64位平台上，`UInt64`长度相同。 |                                             | 无符号类型`UInt`，长度与当前平台的原生字长相同。 |
| Int8   | 1 字节                                                       | -128 到 127                                 |                                                  |
| UInt8  | 1 字节                                                       | 0 到 255                                    |                                                  |
| Int32  | 4 字节                                                       | -2147483648 到 2147483647                   |                                                  |
| UInt32 | 4 字节                                                       | 0 到 4294967295                             |                                                  |
| Int64  | 8 字节                                                       | -9223372036854775808 到 9223372036854775807 |                                                  |
| UInt64 | 8 字节                                                       | 0 到 18446744073709551615                   |                                                  |

| 类型      | 大小   | 区间值                            | 说明                                         |
| --------- | ------ | --------------------------------- | -------------------------------------------- |
| Float     | 4 字节 | 1.2E-38 到 3.4E+38 (~6 digits)    | 32位浮点数                                   |
| Double    | 8 字节 | 2.3E-308 到 1.7E+308 (~15 digits) | 64位浮点数                                   |
| Bool      |        | true、false和nil                  |                                              |
| Character |        |                                   | 字符指的是单个字母，例如：`C`                |
| String    |        |                                   | 字符串是字符的序列集合，例如：`Hello World!` |



## 2.类型别名

类型别名是对当前的类型定义另一个名字，类型别名通过使用 typealias 关键字来定义。语法格式如下：

```swift
typealias newname = type
```

```Swift
import Cocoa
typealias Feet = Int
var distance: Feet = 100
print(distance)
```



## 3.类型安全

Swift 是一个类型安全（type safe）的语言。

由于 Swift 是类型安全的，所以它会在编译你的代码时进行类型检查（type checks），并把不匹配的类型标记为错误。这可以让你在开发的时候尽早发现并修复错误。例如：

```Swift
import Cocoa

var varA = 42
varA = "This is hello"
print(varA)
```

以上程序，会在 Xcode 中报错：

```Swift
error: cannot assign value of type 'String' to type 'Int'
varA = "This is hello"
```



## 4.类型推断

当你要处理不同类型的值时，类型检查可以帮你避免错误。然而，这并不是说你每次声明常量和变量的时候都需要显式指定类型。如果你没有显式指定类型，Swift 会使用类型推断（type inference）来选择合适的类型。

```Swift
import Cocoa

// varA 会被推测为 Int 类型 
var varA = 42
print(varA)

// varB 会被推测为 Double 类型  
var varB = 3.14159
print(varB)

// varC 也会被推测为 Double 类型   
var varC = 3 + 0.14159
print(varC)
```



# 三、`let`、`var`和`Optional`

## 1.变量

变量是一种使用方便的占位符，用于引用计算机内存地址。Swift中每个变量都指定了特定的类型，该类型决定了变量占用内存的大小，不同的数据类型也决定可存储值的范围。在使用变量前，你需要使用 **var** 关键字声明它。

```Swift
import Cocoa

var varA = 42
print(varA)

var varB:Float

varB = 3.14159
print(varB)
```

在字符串中可以使用括号与反斜线来插入变量，如下实例：

```Swift
import Cocoa

var name = "菜鸟教程"
var site = "http://www.runoob.com"

print("\(name)的官网地址为：\(site)")
```

## 2.可选类型（Optional）

Swift 的可选（Optional）类型，用于处理值缺失的情况。Swfit语言定义后缀？作为命名类型Optional的简写，换句话说，以下两种声明是相等的：

```swift
var optionalInteger: Int?
var optionalInteger: Optional<Int>
```

* 强制解析

  当你确定可选类型确实包含值之后，你可以在可选的名字后面加一个感叹号（!）来获取值。这被称为可选值的强制解析（forced unwrapping）。

  ```swift
  import Cocoa
  
  var myString:String?
  
  myString = "Hello, Swift!"
  
  if myString != nil {//强制解析当变量为nil的时候会报错，所以最好先做一下非空判断
     // 强制解析
     print( myString! )
  }else{
     print("myString 值为 nil")
  }
  ```

  

* 自动解析

  你可以在声明可选变量时使用感叹号（!）替换问号（?）。这样可选变量在使用时就不需要再加一个感叹号（!）来获取值，它会自动解析。

  ```swift
  import Cocoa
  
  var myString:String!
  
  myString = "Hello, Swift!"
  
  if myString != nil {
     print(myString)
  }else{
     print("myString 值为 nil")
  }
  ```

  

* 可选绑定

  使用可选绑定（optional binding）来判断可选类型是否包含值，如果包含就把值赋给一个临时常量或者变量。可选绑定可以用在if和while语句中来对可选类型的值进行判断并把值赋给一个常量或者变量。

  ```swift
  import Cocoa
  
  var myString:String?
  
  myString = "Hello, Swift!"
  
  if let yourString = myString {
     print("你的字符串值为 - \(yourString)")
  }else{
     print("你的字符串没有值")
  }
  ```

  

## 3.常量

常量一旦设定，在程序运行时就无法改变其值。常量使用关键字 **let** 来声明。

```swift
import Cocoa

let constA = 42
print(constA)
```

在字符串中可以使用括号与反斜线来插入常量：

```swift
import Cocoa

let name = "菜鸟教程"
let site = "http://www.runoob.com"

print("\(name)的官网地址为：\(site)")
```



## 4.类型标注

当你声明常量或者变量的时候可以加上类型标注（type annotation），说明常量或者变量中要存储的值的类型。如果要添加类型标注，需要在常量或者变量名后面加上一个冒号和空格，然后加上类型名称。

```swift
import Cocoa

var varA: Int = 42
print(constA)

let constB:Float = 3.14159
print(constB)
```



# 四、运算符

运算符是一个符号，用于告诉编译器执行一个数学或逻辑运算。

## 1.算术运算符

| 运算符 | 描述 | 例子             |
| ------ | ---- | ---------------- |
| +      | 加号 | A + B 结果为 30  |
| −      | 减号 | A − B 结果为 -10 |
| *      | 乘号 | A * B 结果为 200 |
| /      | 除号 | B / A 结果为 2   |
| %      | 求余 | B % A 结果为 0   |

**注意：**swift3 中已经取消了***++***、***--***。



## 2.比较运算符

| 运算符 | 描述     | 例子                |
| ------ | -------- | ------------------- |
| ==     | 等于     | (A == B) 为 false。 |
| !=     | 不等于   | (A != B) 为 true。  |
| >      | 大于     | (A > B) 为 false。  |
| <      | 小于     | (A < B) 为 true。   |
| >=     | 大于等于 | (A >= B) 为 false。 |
| <=     | 小于等于 | (A <= B) 为 true。  |



## 3.逻辑运算符

| 运算符 | 描述                                                 | 例子                 |
| ------ | ---------------------------------------------------- | -------------------- |
| &&     | 逻辑与。如果运算符两侧都为 TRUE 则为 TRUE。          | (A && B) 为 false。  |
| \|\|   | 逻辑或。 如果运算符两侧至少有一个为 TRUE 则为 TRUE。 | (A \|\| B) 为 true。 |
| !      | 逻辑非。布尔值取反，使得true变false，false变true。   | !(A && B) 为 true。  |



## 4.位运算符

位运算符用来对二进制位进行操作，~,&,|,^分别为取反，按位与与，按位与或，按位与异或运算，如下表实例：

| p    | q    | p&q  | p\|q | p^q  |
| ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 0    | 0    |
| 0    | 1    | 0    | 1    | 1    |
| 1    | 1    | 1    | 1    | 0    |
| 1    | 0    | 0    | 1    | 1    |

| 运算符 | 描述                                                         | 图解                                                         | 实例                                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| &      | 按位与。按位与运算符对两个数进行操作，然后返回一个新的数，这个数的每个位都需要两个输入数的同一位都为1时才为1。 | ![img](https://www.runoob.com/wp-content/uploads/2015/10/8370_140612144422_1.png) | (A & B) 结果为 12, 二进制为 0000 1100                        |
| \|     | 按位或。按位或运算符\|比较两个数，然后返回一个新的数，这个数的每一位设置1的条件是两个输入数的同一位都不为0(即任意一个为1，或都为1)。 | ![img](https://www.runoob.com/wp-content/uploads/2015/10/8370_140612144511_1.png) | (A \| B) 结果为 61, 二进制为 0011 1101                       |
| ^      | 按位异或. 按位异或运算符^比较两个数，然后返回一个数，这个数的每个位设为1的条件是两个输入数的同一位不同，如果相同就设为0。 | ![img](https://www.runoob.com/wp-content/uploads/2015/10/8370_140612144558_1.png) | (A ^ B) 结果为 49, 二进制为 0011 0001                        |
| ~      | 按位取反运算符~对一个操作数的每一位都取反。                  | ![img](https://www.runoob.com/wp-content/uploads/2015/10/8370_140612144245_1.png) | (~A ) 结果为 -61, 二进制为 1100 0011 in 2's complement form. |
| <<     | 按位左移。左移操作符（<<）将操作数的所有位向左移动指定的位数。 | 下图展示了11111111 << 1（11111111 左移一位）的结果。蓝色数字表示被移动位，灰色表示被丢弃位，空位用橙色的0填充。![img](https://www.runoob.com/wp-content/uploads/2015/10/leftbit.jpg) | A << 2 结果为 240, 二进制为 1111 0000                        |
| >>     | 按位右移。右移操作符（>>）将操作数的所有位向右移动指定的位数。 | 下图展示了11111111 >> 1（11111111 右移一位）的结果。蓝色数字表示被移动位，灰色表示被丢弃位，空位用橙色的0填充。![img](https://www.runoob.com/wp-content/uploads/2015/10/rightbit.jpg) | A >> 2 结果为 15, 二进制为 0000 1111                         |



```swift
import Cocoa

var A = 60  // 二进制为 0011 1100
var B = 13 // 二进制为 0000 1101

print("A&B 结果为：\(A&B)") //12
print("A|B 结果为：\(A|B)") //61
print("A^B 结果为：\(A^B)") //49
print("~A 结果为：\(~A)")	  //-61
```



## 5.赋值运算符

| 运算符 | 描述                                                         | 实例                                  |
| ------ | ------------------------------------------------------------ | ------------------------------------- |
| =      | 简单的赋值运算，指定右边操作数赋值给左边的操作数。           | C = A + B 将 A + B 的运算结果赋值给 C |
| +=     | 相加后再赋值，将左右两边的操作数相加后再赋值给左边的操作数。 | C += A 相当于 C = C + A               |
| -=     | 相减后再赋值，将左右两边的操作数相减后再赋值给左边的操作数。 | C -= A 相当于 C = C - A               |
| *=     | 相乘后再赋值，将左右两边的操作数相乘后再赋值给左边的操作数。 | C *= A 相当于 C = C * A               |
| /=     | 相除后再赋值，将左右两边的操作数相除后再赋值给左边的操作数。 | C /= A 相当于 C = C / A               |
| %=     | 求余后再赋值，将左右两边的操作数求余后再赋值给左边的操作数。 | C %= A is equivalent to C = C % A     |
| <<=    | 按位左移后再赋值                                             | C <<= 2 相当于 C = C << 2             |
| >>=    | 按位右移后再赋值                                             | C >>= 2 相当于 C = C >> 2             |
| &=     | 按位与运算后赋值                                             | C &= 2 相当于 C = C & 2               |

| 运算符 | 描述                   | 实例                      |
| ------ | ---------------------- | ------------------------- |
| ^=     | 按位异或运算符后再赋值 | C ^= 2 相当于 C = C ^ 2   |
| \|=    | 按位或运算后再赋值     | C \|= 2 相当于 C = C \| 2 |



## 6.区间运算符

| 运算符         | 描述                                                         | 实例                           |
| -------------- | ------------------------------------------------------------ | ------------------------------ |
| 闭区间运算符   | 闭区间运算符（a...b）定义一个包含从a到b(包括a和b)的所有值的区间，b必须大于等于a。 ‌ 闭区间运算符在迭代一个区间的所有值时是非常有用的，如在for-in循环中： | 1...5 区间值为 1, 2, 3, 4 和 5 |
| 半开区间运算符 | 半开区间（a..<b）定义一个从a到b但不包括b的区间。 之所以称为半开区间，是因为该区间包含第一个值而不包括最后的值。 | 1..< 5 区间值为 1, 2, 3, 和 4  |

```swift
import Cocoa

print("闭区间运算符:")
for index in 1...5 {
    print("\(index) * 5 = \(index * 5)")
}

print("半开区间运算符:")
for index in 1..<5 {
    print("\(index) * 5 = \(index * 5)")
}
```



## 7.其他运算符

| 运算符     | 描述                  | 实例                                           |
| ---------- | --------------------- | ---------------------------------------------- |
| 一元减     | 数字前添加 - 号前缀   | -3 或 -4                                       |
| 一元加     | 数字前添加 + 号前缀   | +6 结果为 6                                    |
| 三元运算符 | **condition ? X : Y** | 如果 **condition** 为 true ，值为 X ，否则为 Y |



## 8.运算符优先级

基本的优先级需要记住：

- 指针最优，单目运算优于双目运算。如正负号。
- 先乘除（模），后加减。
- 先算术运算，后移位运算，最后位运算。请特别注意：1 << 3 + 2 & 7 等价于 (1 << (3 + 2))&7
- 逻辑运算最后计算

| 运算符         | 实例                |
| -------------- | ------------------- |
| 位运算符       | >> &<< &>> >>       |
| 乘法运算符     | &* % & * /          |
| 加法运算符     | \| &+ &- + -  ^     |
| 区间运算符     | ..< ...             |
| 类型转换运算符 | is as               |
| nil 的聚合运算 | ??                  |
| 比较运算符     | != > < >= <= === == |
| 逻辑与运算符   | &&                  |
| 逻辑或运算符   | \|\|                |

| 运算符     | 实例                                       |
| ---------- | ------------------------------------------ |
| 波浪箭头   | ~>                                         |
| 三元运算符 | ?:                                         |
| 箭头函数   | ( )                                        |
| 赋值运算符 | \|= %= /= &<<= &>>= &= *= >>= <<= ^= += -= |

# 五、逻辑控制

## 1.条件语句

| 语句                     | 描述                                                         |
| :----------------------- | :----------------------------------------------------------- |
| if 语句                  | **if 语句** 由一个布尔表达式和一个或多个执行语句组成。       |
| if...else 语句           | **if 语句** 后可以有可选的 **else 语句**, **else 语句**在布尔表达式为 false 时执行。 |
| if...else if...else 语句 | **if** 后可以有可选的 **else if...else** 语句, **else if...else** 语句常用于多个条件判断。 |
| 内嵌 if 语句             | 你可以在 **if** 或 **else if** 中内嵌 **if** 或 **else if** 语句。 |
| switch 语句              | switch 语句允许测试一个变量等于多个值时的情况。              |
| 三元运算符               | **condition ? X : Y**                                        |



## 2.循环控制

| 循环类型            | 描述                                                         |
| :------------------ | :----------------------------------------------------------- |
| for-in              | 遍历一个集合里面的所有元素，例如由数字表示的区间、数组中的元素、字符串中的字符。 |
| for 循环            | 该循环方式在 Swift 3 中已经弃用。用来重复执行一系列语句直到达成特定条件达成，一般通过在每次循环完成后增加计数器的值来实现。 |
| while 循环          | 运行一系列语句，如果条件为true，会重复运行，直到条件变为false。 |
| repeat...while 循环 | 类似 while 语句区别在于判断循环条件之前，先执行一次循环的代码块。 |

| 控制语句         | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| continue 语句    | 告诉一个循环体立刻停止本次循环迭代，重新开始下次循环迭代。   |
| break 语句       | 中断当前循环。                                               |
| fallthrough 语句 | 如果在一个case执行完后，继续执行下面的case，需要使用fallthrough(贯穿)关键字。 |

# 六、字符串

字符串常用函数/运算符：

| 序号 | 函数/运算符 & 描述                                           |
| :--- | :----------------------------------------------------------- |
| 1    | **isEmpty**判断字符串是否为空，返回布尔值                    |
| 2    | **hasPrefix(prefix: String)**检查字符串是否拥有特定前缀      |
| 3    | **hasSuffix(suffix: String)**检查字符串是否拥有特定后缀。    |
| 4    | **Int(String)**转换字符串数字为整型。 实例: `let myString: String = "256" let myInt: Int? = Int(myString)` |
| 5    | **String.count** **Swift 3 版本使用的是 String.characters.count**计算字符串的长度 |
| 6    | **utf8**您可以通过遍历 String 的 utf8 属性来访问它的 UTF-8 编码 |
| 7    | **utf16**您可以通过遍历 String 的 utf8 属性来访问它的 utf16 编码 |
| 8    | **unicodeScalars**您可以通过遍历String值的unicodeScalars属性来访问它的 Unicode 标量编码. |
| 9    | **+**连接两个字符串，并返回一个新的字符串                    |
| 10   | **+=**连接操作符两边的字符串并将新字符串赋值给左边的操作符变量 |
| 11   | **==**判断两个字符串是否相等                                 |
| 12   | **<**比较两个字符串，对两个字符串的字母逐一比较。            |
| 13   | **!=**比较两个字符串是否不相等。                             |

转义字符：

| 转义字符 | 含义                             |
| -------- | -------------------------------- |
| \0       | 空字符                           |
| `\\`     | 反斜线 \                         |
| \b       | 退格(BS) ，将当前位置移到前一列  |
| \f       | 换页(FF)，将当前位置移到下页开头 |
| \n       | 换行符                           |
| \r       | 回车符                           |
| \t       | 水平制表符                       |
| \v       | 垂直制表符                       |
| `\'`     | 单引号                           |

| 转义字符 | 含义                           |      |
| -------- | ------------------------------ | ---- |
| `\"`     | 双引号                         |      |
| \000     | 1到3位八进制数所代表的任意字符 |      |
| \xhh...  | 1到2位十六进制所代表的任意字符 |      |

# 七、数组

Swift 数组使用有序列表存储同一类型的多个值。相同的值可以多次出现在一个数组的不同位置中。Swift 数组会强制检测元素的类型，如果类型不同则会报错，Swift 数组应该遵循像Array<Element>这样的形式，其中Element是这个数组中唯一允许存在的数据类型。

如果创建一个数组，并赋值给一个变量，则创建的集合就是可以修改的。这意味着在创建数组后，可以通过添加、删除、修改的方式改变数组里的项目。如果将一个数组赋值给常量，数组就不可更改，并且数组的大小和内容都不可以修改。

## 1.创建数组

```swift
var someArray = [SomeType]()
```

```swift
var someArray = [SomeType](repeating: InitialValue, count: NumbeOfElements)
```

```swift
var someInts = [Int](repeating: 0, count: 3)
```

```swift
var someInts:[Int] = [10, 20, 30]
```



## 2.`append`和`+=`

使用 append() 方法或者赋值运算符 += 在数组末尾添加元素。

```swift
import Cocoa

var someInts = [Int]()

someInts.append(20)
someInts.append(30)
someInts += [40]

var someVar = someInts[0]

print( "第一个元素的值 \(someVar)" )
print( "第二个元素的值 \(someInts[1])" )
print( "第三个元素的值 \(someInts[2])" )
```

## 3.合并数组

使用加法操作符（+）来合并两种已存在的相同类型数组。

```swift
import Cocoa

var intsA = [Int](repeating: 2, count:2)
var intsB = [Int](repeating: 1, count:3)

var intsC = intsA + intsB

for item in intsC {
    print(item)
}
```



## 4.数组的`count`属性和`isEmpty`属性

使用 count 属性来计算数组元素个数：

```swift
import Cocoa

var intsA = [Int](count:2, repeatedValue: 2)
var intsB = [Int](count:3, repeatedValue: 1)

var intsC = intsA + intsB

print("intsA 元素个数为 \(intsA.count)")
print("intsB 元素个数为 \(intsB.count)")
print("intsC 元素个数为 \(intsC.count)")
```

通过只读属性 isEmpty 来判断数组是否为空，返回布尔值：

```swift
import Cocoa

var intsA = [Int](count:2, repeatedValue: 2)
var intsB = [Int](count:3, repeatedValue: 1)
var intsC = [Int]()

print("intsA.isEmpty = \(intsA.isEmpty)")
print("intsB.isEmpty = \(intsB.isEmpty)")
print("intsC.isEmpty = \(intsC.isEmpty)")
```

# 八、元组

元组与数组类似，不同的是，元组中的元素可以是任意类型。以下是两种元组定义方式：

```swift
let tuple: (Int, String) = (10, "season")
print(tuple)
print(tuple.0)
print(tuple.1)
//key-value形式
var tuple: (age: Int, name: String) = (10, "season")
print(tuple.age)
print(tuple.name)
```

# 九、字典

Swift 字典用来存储无序的相同类型数据的集合，Swift 字典会强制检测元素的类型，如果类型不同则会报错。Swift 字典每个值（value）都关联唯一的键（key），键作为字典中的这个值数据的标识符。如果创建一个字典，并赋值给一个变量，则创建的字典就是可以修改的。这意味着在创建字典后，可以通过添加、删除、修改的方式改变字典里的项目。如果将一个字典赋值给常量，字典就不可修改，并且字典的大小和内容都不可以修改。

## 1.创建字典

```swift
//格式
var someDict =  [KeyType: ValueType]()
//例子
var someDict = [Int: String]()
var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]
```



## 2.访问和修改字典元素

```swift
var someVar = someDict[key]
```

```swift
import Cocoa

var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]

var oldVal = someDict[1]
//将字典key为1的元素值改为"One 新的值"
someDict[1] = "One 新的值"
var someVar = someDict[1]

print( "key = 1 的值为 \(someVar)" )
print( "key = 2 的值为 \(someDict[2])" )
print( "key = 3 的值为 \(someDict[3])" )
```



## 3.移除字典元素

可以使用 **removeValueForKey()** 方法来移除字典 key-value 对。如果 key 存在该方法返回移除的值，如果不存在返回 nil 。也可以通过指定键的值为 nil 来移除 key-value（键-值）对。

```swift
import Cocoa

var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]

var removedValue = someDict.removeValue(forKey: 2)
someDict[2] = nil

print( "key = 1 的值为 \(someDict[1])" )
print( "key = 2 的值为 \(someDict[2])" )
print( "key = 3 的值为 \(someDict[3])" )
```

输出结果为：

```swift
key = 1 的值为 Optional("One")
key = 2 的值为 nil
key = 3 的值为 Optional("Three")
```



## 4.遍历字典

可以使用 **for-in** 循环来遍历某个字典中的键值对。

```swift
import Cocoa

var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]

for (key, value) in someDict {
   print("字典 key \(key) -  字典 value \(value)")
}
```

也可以使用enumerate()方法来进行字典遍历，返回的是字典的索引及 (key, value) 对。

```swift
import Cocoa

var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]

for (key, value) in someDict.enumerated() {
    print("字典 key \(key) -  字典 (key, value) 对 \(value)")
}
```



## 5.字典转为数组

通过`.keys`和`.values`属性分别提取字典的key数组和value数组：

```swift
import Cocoa

var someDict:[Int:String] = [1:"One", 2:"Two", 3:"Three"]

let dictKeys = [Int](someDict.keys)
let dictValues = [String](someDict.values)

print("输出字典的键(key)")

for (key) in dictKeys {
    print("\(key)")
}

print("输出字典的值(value)")

for (value) in dictValues {
    print("\(value)")
}
```

## 6.字典的`count`属性和`isEmpty`属性

以使用只读的 **count** 属性来计算字典有多少个键值对：

```swift
import Cocoa

var someDict1:[Int:String] = [1:"One", 2:"Two", 3:"Three"]
var someDict2:[Int:String] = [4:"Four", 5:"Five"]

print("someDict1 含有 \(someDict1.count) 个键值对")
print("someDict2 含有 \(someDict2.count) 个键值对")
```

可以通过只读属性 **isEmpty** 来判断字典是否为空，返回布尔值:

```swift
import Cocoa

var someDict1:[Int:String] = [1:"One", 2:"Two", 3:"Three"]
var someDict2:[Int:String] = [4:"Four", 5:"Five"]
var someDict3:[Int:String] = [Int:String]()

print("someDict1 = \(someDict1.isEmpty)")
print("someDict2 = \(someDict2.isEmpty)")
print("someDict3 = \(someDict3.isEmpty)")
```

# 十、函数

## 1.函数定义

Swift 定义函数使用关键字 **func**。函数参数都有一个外部参数名和一个局部参数名。语法格式如下：

```swift
func funcname(外部参数名 内部参数名: 参数类型,...) -> returntype
{
   Statement1
   Statement2
   ……
   Statement N
   return parameters
}
```

```swift
import Cocoa

//带参数的函数
func runoob(site: String) -> String {
    return (site)
}
print(runoob(site: "www.runoob.com"))

//不带参数的函数
func funcname() -> datatype {
   return datatype
}
print(sitename())
//外部参数名和内部参数名分开写法
func pow(firstArg a: Int, secondArg b: Int) -> Int {
   var res = a
   for _ in 1..<b {
      res = res * a
   }
   print(res)
   return res
}
pow(firstArg:5, secondArg:3)
//不提供外部参数名的写法
func pow(_ a: Int, _ b: Int) -> Int {
   var res = a
   for _ in 1..<b {
      res = res * a
   }
   print(res)
   return res
}
pow(5, 3)
```



## 2.可变参数

可变参数可以接受零个或多个值。函数调用时，你可以用可变参数来指定函数参数，其数量是不确定的。

```swift
import Cocoa

func vari<N>(members: N...){
    for i in members {
        print(i)
    }
}
vari(members: 4,3,5)
vari(members: 4.5, 3.1, 5.6)
vari(members: "Google", "Baidu", "Runoob")
```

## 3.常量参数和变量参数

一般默认在函数中定义的参数都是常量参数，也就是这个参数你只可以查询使用，不能改变它的值。如果想要声明一个变量参数，可以在参数定义前加 `inout `关键字，这样就可以改变这个参数的值了。因为一般默认的参数传递都是传值调用的，而不是传引用，所以传入的参数在函数内改变，并不影响原来的那个参数，传入的只是这个参数的副本。当传入的参数作为输入输出参数时，需要在参数名前加 & 符号，表示这个值可以被函数修改。

```swift
import Cocoa

func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}


var x = 1
var y = 5
swapTwoInts(&x, &y)
print("x 现在的值 \(x), y 现在的值 \(y)")
```

## 4.函数类型

在 Swift 中，使用函数类型就像使用其他类型一样。函数类型可作为函数的参数类型和返回类型使用。

```swift
import Cocoa

func sum(a: Int, b: Int) -> Int {
   return a + b
}
var addition: (Int, Int) -> Int = sum
print("输出结果: \(addition(40, 89))")
```

## 5.函数㠌套

函数嵌套指的是函数内定义一个新的函数，外部的函数可以调用函数内定义的函数。

```swift
import Cocoa

func sum(a: Int, b: Int) -> Int {
    return a + b
}
var addition: (Int, Int) -> Int = sum
print("输出结果: \(addition(40, 89))")

func another(addition: (Int, Int) -> Int, a: Int, b: Int) {
    print("输出结果: \(addition(a, b))")
}
another(addition: sum, a: 10, b: 20)
```

## 6.函数重载

方法名相同,但是参数列表不同. 这样同名不同参的函数之间互相称之为重载函数.

# 十一、闭包

闭包(Closures)是自包含的功能代码块，可以在代码中使用或者用来作为参数传值。Swift 中的闭包与 C 和 Objective-C 中的代码块（blocks）以及其他一些编程语言中的 匿名函数比较相似。Swift中的闭包有很多优化的地方:

* 根据上下文推断参数和返回值类型
* 从单行表达式闭包中隐式返回（也就是闭包体只有一行代码，可以省略return）
* 可以使用简化参数名，如$0, $1(从0开始，表示第i个参数...)
* 提供了尾随闭包语法(Trailing closure syntax)

函数和闭包都是引用类型。无论您将函数/闭包赋值给一个常量还是变量，实际上都是将常量/变量的值设置为对应函数/闭包的引用。这也意味着如果您将闭包赋值给了两个不同的常量/变量，两个值都会指向同一个闭包。

## 1.闭包的写法

语法格式：

```swift
{(parameters) -> return type in
   statements
}
```

```swift
import Cocoa

//无参数无返回值闭包写法
let studname = { print("Swift 闭包实例。") }
studname()

//带参数和返回值闭包常规写法
let divide = {(val1: Int, val2: Int) -> Int in 
   return val1 / val2 
}
let result = divide(200, 20)
print (result)

//使用参数名称缩写和隐式返回值的写法
let names = ["AT", "AE", "D", "S", "BE"]
var reversed = names.sorted( by: { $0 > $1 } )
print(reversed)

//运算符函数自动推断写法
let names = ["AT", "AE", "D", "S", "BE"]
var reversed = names.sorted(by: >)
print(reversed)


```

## 2.尾随闭包

尾随闭包是一个书写在函数括号之后的闭包表达式，函数支持将其作为最后一个参数调用。

```swift
func someFunctionThatTakesAClosure(closure: () -> Void) {
    // 函数体部分
}

// 以下是不使用尾随闭包进行函数调用
someFunctionThatTakesAClosure({
    // 闭包主体部分
})

// 以下是使用尾随闭包进行函数调用
someFunctionThatTakesAClosure() {
  // 闭包主体部分
}
```

```swift
import Cocoa

let names = ["AT", "AE", "D", "S", "BE"]

//尾随闭包
var reversed = names.sorted() { $0 > $1 }
print(reversed)
```

## 3.捕获值

1. 闭包可以在其定义的上下文中捕获常量或变量。即使定义这些常量和变量的原域已经不存在，闭包仍然可以在闭包函数体内引用和修改这些值。

2. Swift最简单的闭包形式是嵌套函数，也就是定义在其他函数的函数体内的函数。嵌套函数可以捕获其外部函数所有的参数以及定义的常量和变量。

3. ```swift
   import Cocoa
   
   func makeIncrementor(forIncrement amount: Int) -> () -> Int {
       var runningTotal = 0
       func incrementor() -> Int {
           runningTotal += amount
           return runningTotal
       }
       return incrementor
   }
   
   let incrementByTen = makeIncrementor(forIncrement: 10)
   
   // 返回的值为10
   print(incrementByTen())
   
   // 返回的值为20
   print(incrementByTen())
   
   // 返回的值为30
   print(incrementByTen())
   ```

## 4.逃逸闭包

当闭包作为一个实际参数传递给一个函数的时候，并且是在函数返回之后调用，我们就说这个闭包逃逸了。当我们声明一个接受闭包作为形式参数的函数时，你可以在形式参数前写 `@escaping` 来明确闭包是允许逃逸的。不需要在函数结束前被调用，可以等到特定时机时才被调用。

```swift
class Closure{
    var handle: ((Int) -> Void)?

    func test(_ a: Int, handler: @escaping (Int) -> Void) {
        self.handle = handler
    }
}
```



## 5.自动闭包

* 自动闭包是一种自动创建的闭包，用于包装传递给函数作为参数的表达式。

* 这种闭包不接受任何参数，当它被调用的时候，会返回被包装在其中的表达式的值。

* 这种便利语法让你能够省略闭包的花括号，用一个普通的表达式来代替显式的闭包。

* 自动闭包让你能够延迟求值，因为直到你调用这个闭包，代码段才会被执行。

* 延迟求值对于那些有副作用（Side Effect）和高计算成本的代码来说是很有益处的，因为它使得你能控制代码的执行时机。

通过将参数标记为 `@autoclosure` 来接收一个自动闭包。

```swift
// serve(element:) 函数接受一个返回元素的显式的闭包。
func serve(element elementProvider: () -> String) {
    print("debug \(elementProvider())!")
}

serve(element: { dataArr.remove(at: 0) } )
// 打印出“debug Alex!”
```

```swift
func serve(element elementProvider: @autoclosure () -> String) {
    print("debug \(elementProvider())!")
}
serve(element: dataArr.remove(at: 0))
```

# 十二、枚举、结构体和类

## 1.枚举

枚举简单的说也是一种数据类型，只不过是这种数据类型只包含自定义的特定数据，它是一组有共同特性的数据的集合。

Swift 的枚举类似于 Objective C 和 C 的结构，枚举的功能为:

- 它声明在类中，可以通过实例化类来访问它的值。
- 枚举也可以定义构造函数（initializers）来提供一个初始成员值；可以在原始的实现基础上扩展它们的功能。
- 可以遵守协议（protocols）来提供标准的功能。

### 1.1定义

语法：

```swift
enum enumname {
   // 枚举定义放在这里
}
```

```swift
// 定义枚举
enum DaysofaWeek {
    case Sunday
    case Monday
    case TUESDAY
    case WEDNESDAY
    case THURSDAY
    case FRIDAY
    case Saturday
}
enum Season {
    case spring,summer,autumn,winter
}
```

### 1.2 关联值

Swift中的枚举可以存储任意确定类型的关联值，这些值被称为枚举关联值。

```swift
enum Code{
    case num(Int,Int,Int)
    case str(String,String)
}
var code = Code.num(2, 3, 3)
code =  .str("A", "B")

switch code {
case .num(let num1, let num2, let num3):
    print("\(num1),\(num2),\(num3)")
case .str(let str1, let str2):
    print("\(str1),\(str2)")
}
```



### 1.3原始值

枚举的原始值可以是字符串，字符，或者任何整型值或浮点型值。每个原始值在它的枚举声明中必须是唯一的。在原始值为整数的枚举时，不需要显式的为每一个成员赋值，Swift会自动为你赋值。

```swift
enum Month: Int {
    case January = 1, February, March, April, May, June, July, August, September, October, November, December
}

let yearMonth = Month.May.rawValue
print("数字月份为: \(yearMonth)。")
```



***注意: 原始值和关联值是不同的。原始值是在定义枚举时被预先填充的值。对于一个特定的枚举成员，它的原始值始终不变。关联值是创建一个基于枚举成员的常量或变量时才设置的值，枚举成员的关联值可以变化。***

## 2.结构体

通过关键字 struct 来定义结构体：

```swift
struct studentMarks {
   var mark1 = 100
   var mark2 = 78
   var mark3 = 98
}
let marks = studentMarks()
print("Mark1 是 \(marks.mark1)")
print("Mark2 是 \(marks.mark2)")
print("Mark3 是 \(marks.mark3)")
```

**注意：一个结构体实例在赋值或传递时，封装的数据将会被拷贝而不是被引用，任何在结构体中储存的值类型属性，也将会被拷贝，而不是被引用。**

```swift
struct MarksStruct {
   var mark: Int

   init(mark: Int) {
      self.mark = mark
   }
}
var aStruct = MarksStruct(mark: 98)
var bStruct = aStruct // aStruct 和 bStruct 是使用相同值的结构体！
bStruct.mark = 97
print(aStruct.mark) // 98
print(bStruct.mark) // 97
```



## 3.类

类是构建代码所用的一种通用且灵活的构造体。Swift通过`class`关键字来定义类：

```swift
class student{
   var studname: String
   var mark: Int 
   var mark2: Int 
}
```

因为类是引用类型，有可能有多个常量和变量在后台同时引用某一个类实例。为了能够判定两个常量或者变量是否引用同一个类实例，Swift 内建了两个恒等运算符：

| **恒等运算符**                                  | **不恒等运算符**                                  |
| :---------------------------------------------- | :------------------------------------------------ |
| 运算符为：===                                   | 运算符为：!==                                     |
| 如果两个常量或者变量引用同一个类实例则返回 true | 如果两个常量或者变量引用不同一个类实例则返回 true |

```swift
class SampleClass: Equatable {
    let myProperty: String
    init(s: String) {
        myProperty = s
    }
}
let spClass1 = SampleClass(s: "Hello")
let spClass2 = SampleClass(s: "Hello")

if spClass1 === spClass2 {// false
    print("引用相同的类实例 \(spClass1)")
}

if spClass1 !== spClass2 {// true
    print("引用不相同的类实例 \(spClass2)")
}
```



## 4.属性

属性可分为存储属性和计算属性:

| **存储属性**                   | **计算属性**             |
| :----------------------------- | :----------------------- |
| 存储常量或变量作为实例的一部分 | 计算（而不是存储）一个值 |
| 用于类和结构体                 | 用于类、结构体和枚举     |

存储属性和计算属性通常用于特定类型的实例。另外，还可以定义属性观察器来监控属性值的变化，以此来触发一个自定义的操作。属性观察器可以添加到自己写的存储属性上，也可以添加到从父类继承的属性上。

### 4.1 存储属性

简单来说，一个存储属性就是存储在特定类或结构体的实例里的一个常量或变量。存储属性可以是变量存储属性（用关键字var定义），也可以是常量存储属性（用关键字let定义）。

- 可以在定义存储属性的时候指定默认值
- 也可以在构造过程中设置或修改存储属性的值，甚至修改常量存储属性的值

```swift
struct Number
{
   var digits: Int
   let pi = 3.1415
}

var n = Number(digits: 12345)
n.digits = 67

print("\(n.digits)")
print("\(n.pi)")
```

**延迟存储属性**

延迟存储属性是指当第一次被调用的时候才会计算其初始值的属性。在属性声明前使用 **lazy** 来标示一个延迟存储属性。

```swift
class sample {
    lazy var no = number() // `var` 关键字是必须的
}

class number {
    var name = "Runoob Swift 教程"
}

var firstsample = sample()
print(firstsample.no.name)
```

***注意：必须将延迟存储属性声明成变量（使用*`var`*关键字），因为属性的值在实例构造完成之前可能无法得到。而常量属性在构造过程完成之前必须要有初始值，因此无法声明成延迟属性。***

### 4.2 计算属性

除存储属性外，类、结构体和枚举可以定义*计算属性*，计算属性不直接存储值，而是提供一个 getter 来获取值，一个可选的 setter 来间接设置其他属性或变量的值。只有 getter 没有 setter 的计算属性就是只读计算属性。只读计算属性总是返回一个值，可以通过点(.)运算符访问，但不能设置新的值。

```swift
class sample {
    var no1 = 0.0, no2 = 0.0
    var length = 300.0, breadth = 150.0
    
    var middle: (Double, Double) {
        get{
            return (length / 2, breadth / 2)
        }
        set(axis){
            no1 = axis.0 - (length / 2)
            no2 = axis.1 - (breadth / 2)
        }
    }
}

var result = sample()
print(result.middle)
result.middle = (0.0, 10.0)

print(result.no1)
print(result.no2)
```

***注意：必须使用`var`关键字定义计算属性，包括只读计算属性，因为它们的值不是固定的。`let`关键字只用来声明常量属性，表示初始化后再也无法修改的值。***



### 4.3 属性观察器

属性观察器监控和响应属性值的变化，每次属性被设置值的时候都会调用属性观察器，甚至新的值和现在的值相同的时候也不例外。可以为除了延迟存储属性之外的其他存储属性添加属性观察器，也可以通过重载属性的方式为继承的属性（包括存储属性和计算属性）添加属性观察器。可以为属性添加如下的一个或全部观察器：

- `willSet`在设置新的值之前调用
- `didSet`在新的值被设置之后立即调用
- willSet和didSet观察器在属性初始化过程中不会被调用

```swift
class Samplepgm {
    var counter: Int = 0{
        willSet(newTotal){
            print("计数器: \(newTotal)")
        }
        didSet{
            if counter > oldValue {
                print("新增数 \(counter - oldValue)")
            }
        }
    }
}
let NewCounter = Samplepgm()
NewCounter.counter = 100
NewCounter.counter = 800
```

计算属性和属性观察器所描述的模式也可以用于全局变量和局部变量。

| **局部变量**                       | **全局变量**                               |
| :--------------------------------- | :----------------------------------------- |
| 在函数、方法或闭包内部定义的变量。 | 函数、方法、闭包或任何类型之外定义的变量。 |
| 用于存储和检索值。                 | 用于存储和检索值。                         |
| 存储属性用于获取和设置值。         | 存储属性用于获取和设置值。                 |
| 也用于计算属性。                   | 也用于计算属性。                           |

### 4.4 类型属性

使用关键字 static 来定义值类型的类型属性，关键字 class 来为类定义类型属性。

```swift
struct Structname {
   static var storedTypeProperty = " "
   static var computedTypeProperty: Int {
      // 这里返回一个 Int 值
   }
}

enum Enumname {
   static var storedTypeProperty = " "
   static var computedTypeProperty: Int {
      // 这里返回一个 Int 值
   }
}

class Classname {
   class var computedTypeProperty: Int {
      // 这里返回一个 Int 值
   }
}
```



## 5.方法

在 Objective-C 中，类是唯一能定义方法的类型。但在 Swift 中，你不仅能选择是否要定义一个类/结构体/枚举，还能灵活的在你创建的类型（类/结构体/枚举）上定义方法。与函数参数一样可以同时有一个局部名称（在函数体内部使用）和一个外部名称（在调用函数时使用），也可以使用下划线（_）设置参数不提供一个外部名称。

```swift
class multiplication {
    var count: Int = 0
    func incrementBy(first no1: Int, _ no2: Int) {
        count = no1 * no2
        print(count)
    }
}

let counter = multiplication()
counter.incrementBy(first: 800, 3)
counter.incrementBy(first: 100, 5)
counter.incrementBy(first: 15000, 3)
```

### 5.1可变方法

Swift 语言中结构体和枚举是值类型。一般情况下，值类型的属性不能在它的实例方法中被修改。但是，如果你确实需要在某个具体的方法中修改结构体或者枚举的属性，你可以选择变异(mutating)这个方法，然后方法就可以从方法内部改变它的属性；并且它做的任何改变在方法结束时还会保留在原始结构中。方法还可以给它隐含的self属性赋值一个全新的实例，这个新实例在方法结束后将替换原来的实例。

```swift
struct area {
    var length = 1
    var breadth = 1
    
    func area() -> Int {
        return length * breadth
    }
    
    mutating func scaleBy(res: Int) {
        self.length *= res
        self.breadth *= res
        print(length)
        print(breadth)
    }
}
var val = area(length: 3, breadth: 5)
val.scaleBy(res: 13)
```



### 5.2类型方法

实例方法是被类型的某个实例调用的方法，你也可以定义类型本身调用的方法，这种方法就叫做类型方法。声明结构体和枚举的类型方法，在方法的func关键字之前加上关键字static。类可能会用关键字class来允许子类重写父类的实现方法。

```swift
class Math
{
    class func abs(number: Int) -> Int
    {
        if number < 0
        {
            return (-number)
        }
        else
        {
            return number
        }
    }
}

struct absno
{
    static func abs(number: Int) -> Int
    {
        if number < 0
        {
            return (-number)
        }
        else
        {
            return number
        }
    }
}

let no = Math.abs(number: -35)
let num = absno.abs(number: -5)

print(no)
print(num)
```



## 6.下标脚本

下标脚本可以定义在类（Class）、结构体（structure）和枚举（enumeration）这些目标中，可以认为是访问对象、集合或序列的快捷方式，不需要再调用实例的特定的赋值和访问方法。定义下标脚本使用`subscript`关键字，显式声明入参（一个或多个）和返回类型。与实例方法不同的是下标脚本可以设定为读写或只读。这种方式又有点像计算型属性的getter和setter：

```swift
class daysofaweek {
    private var days = ["Sunday", "Monday", "Tuesday", "Wednesday",
        "Thursday", "Friday", "saturday"]
    subscript(index: Int) -> String {
        get {
            return days[index]   // 声明下标脚本的值
        }
        set(newValue) {
            self.days[index] = newValue   // 执行赋值操作
        }
    }
}
var p = daysofaweek()

print(p[0])
print(p[1])
print(p[2])
print(p[3])
```

下标脚本允许任意数量的入参索引，并且每个入参类型也没有限制。下标脚本的返回值也可以是任何类型。下标脚本可以使用变量参数和可变参数。一个类或结构体可以根据自身需要提供多个下标脚本实现，在定义下标脚本时通过传入参数的类型进行区分，使用下标脚本时会自动匹配合适的下标脚本实现运行，这就是**下标脚本的重载**。

## 7.构造过程

构造过程是为了使用某个类、结构体或枚举类型的实例而进行的准备过程。这个过程包含了为实例中的每个属性设置初始值和为其执行必要的准备和初始化任务。

### 7.1构造器

Swift 构造函数使用 init() 方法。类和结构体在实例创建时，必须为所有存储型属性设置合适的初始值。存储属性在构造器中赋值时，它们的值是被直接设置的，不会触发任何属性观测器。

```swift
struct Rectangle {
    var length: Double?
  
  	//默认构造器
  	init(){}
    
    init(frombreadth breadth: Double) {
        length = breadth * 10
    }
    
    init(frombre bre: Double) {
        length = bre * 30
    }
    
    init(_ area: Double) {
        length = area
    }
}

let rectarea = Rectangle(180.0)
print("面积为：\(rectarea.length)")

let rearea = Rectangle(370.0)
print("面积为：\(rearea.length)")

let recarea = Rectangle(110.0)
print("面积为：\(recarea.length)")
```



### 7.2结构体的逐一成员构造器

如果结构体对所有存储型属性提供了默认值且自身没有提供定制的构造器，它们能自动获得一个逐一成员构造器。我们在调用逐一成员构造器时，通过与成员属性名相同的参数名进行传值来完成对成员属性的初始赋值。

```swift
struct Rectangle {
    var length = 100.0, breadth = 200.0
}
let area = Rectangle(length: 24.0, breadth: 32.0)

print("矩形的面积: \(area.length)")
print("矩形的面积: \(area.breadth)")
```

### 7.3常量属性初始化

只要在构造过程结束前常量的值能确定，你可以在构造过程中的任意时间点修改常量属性的值。对某个类实例来说，它的常量属性只能在定义它的类的构造过程中修改；不能在子类中修改。

```swift
struct Rectangle {
    let length: Double?
    
    init(frombreadth breadth: Double) {
        length = breadth * 10
    }
    
    init(frombre bre: Double) {
        length = bre * 30
    }
    
    init(_ area: Double) {
        length = area
    }
}
```



### 7.4构造器代理

构造器可以通过调用其它构造器来完成实例的部分构造过程。这一过程称为构造器代理，它能减少多个构造器间的代码重复。

```swift
struct Size {
    var width = 0.0, height = 0.0
}
struct Point {
    var x = 0.0, y = 0.0
}

struct Rect {
    var origin = Point()
    var size = Size()
    init() {}
    init(origin: Point, size: Size) {
        self.origin = origin
        self.size = size
    }
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}
```

***构造器代理规则***

| 值类型                                                       | 类类型                                                       |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| 不支持继承，所以构造器代理的过程相对简单，因为它们只能代理给本身提供的其它构造器。 你可以使用self.init在自定义的构造器中引用其它的属于相同值类型的构造器。 | 它可以继承自其它类,这意味着类有责任保证其所有继承的存储型属性在构造时也能正确的初始化。 |



### 7.5类的构造过程

Swift 提供了两种类型的类构造器来确保所有类实例中存储型属性都能获得初始值，它们分别是指定构造器和便利构造器。

| 指定构造器                                                   | 便利构造器                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 类中最主要的构造器                                           | 类中比较次要的、辅助型的构造器                               |
| 初始化类中提供的所有属性，并根据父类链往上调用父类的构造器来实现父类的初始化。 | 可以定义便利构造器来调用同一个类中的指定构造器，并为其参数提供默认值。你也可以定义便利构造器来创建一个特殊用途或特定输入的实例。 |
| 每一个类都必须拥有至少一个指定构造器                         | 只在必要的时候为类提供便利构造器                             |
| `init(parameters) {    statements }`                         | `convenience init(parameters) {      statements }`           |

```swift
class MainClass {
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    convenience init() {
        self.init(name: "[匿名]")
    }
}

class SubClass: MainClass {
    var count: Int
    init(name: String, count: Int) {
        self.count = count
        super.init(name: name)
    }
    
    override convenience init(name: String) {
        self.init(name: name, count: 1)
    }
}
```



### 7.6类的可失败构造器

如果一个类，结构体或枚举类型的对象，在构造自身的过程中有可能失败，则为其定义一个可失败构造器。可以在一个类，结构体或是枚举类型的定义中，添加一个或多个可失败构造器。其语法为在init关键字后面加添问号(init?)。

```swift
struct Animal {
    let species: String
    init?(species: String) {
        if species.isEmpty { return nil }
        self.species = species
    }
}

enum TemperatureUnit {
    // 开尔文，摄氏，华氏
    case Kelvin, Celsius, Fahrenheit
    init?(symbol: Character) {
        switch symbol {
        case "K":
            self = .Kelvin
        case "C":
            self = .Celsius
        case "F":
            self = .Fahrenheit
        default:
            return nil
        }
    }
}

class StudRecord {
    let studname: String!
    init?(studname: String) {
        self.studname = studname
        if studname.isEmpty { return nil }
    }
}
if let stname = StudRecord(studname: "失败构造器") {
    print("模块为 \(stname.studname)")
}
```

也可以使用通过在init后面添加惊叹号的方式来定义一个可失败构造器(init!):

```swift
struct StudRecord {
    let stname: String
    
    init!(stname: String) {
        if stname.isEmpty {return nil }
        self.stname = stname
    }
}

let stmark = StudRecord(stname: "Runoob")
if let name = stmark {
    print("指定了学生名")
}

let blankname = StudRecord(stname: "")
if blankname == nil {
    print("学生名为空")
}
```



## 8.析构过程

在一个类的实例被释放之前，析构函数被立即调用。用关键字`deinit`来标示析构函数，类似于初始化函数用`init`来标示。析构函数只适用于类类型。

```swift
var counter = 0;  // 引用计数器
class BaseClass {
    init() {
        counter += 1;
    }
    deinit {
        counter -= 1;
    }
}

var show: BaseClass? = BaseClass()
print(counter)
show = nil
print(counter)
```

# 十三、继承

当一个类继承其它类时，继承类叫子类，被继承类叫超类（或父类)。在 Swift 中，子类可以调用和访问超类的方法，属性和下标脚本，并且可以重写它们，也可以为类中继承来的属性添加属性观察器。没有继承其它类的类，称之为基类（Base Class）。

```swift
class StudDetails
{
    var mark1: Int;
    var mark2: Int;
    
    init(stm1:Int, results stm2:Int)
    {
        mark1 = stm1;
        mark2 = stm2;
    }
    
    func show()
    {
        print("Mark1:\(self.mark1), Mark2:\(self.mark2)")
    }
}

class Tom : StudDetails
{
    init()
    {
        super.init(stm1: 93, results: 89)
    }
}

let tom = Tom()
tom.show()
```



## 1.`super`关键字

使用super前缀来访问超类的方法，属性或下标脚本。

| 重写     | 访问方法，属性，下标脚本 |
| :------- | :----------------------- |
| 方法     | super.somemethod()       |
| 属性     | super.someProperty()     |
| 下标脚本 | super[someIndex]         |

## 2.重写

使用 override 关键字来实现重写。如果不希望属性或方法被子类重写，可以使用 final 关键字防止它们被重写。

```swift
class SuperClass {
    func show() {
        print("这是超类 SuperClass")
    }
}

class SubClass: SuperClass  {
    override func show() {
        print("这是子类 SubClass")
    }
}

let superClass = SuperClass()
superClass.show()

let subClass = SubClass()
subClass.show()
```

子类可以提供定制的 getter（或 setter）来重写任意继承来的属性，无论继承来的属性是存储型的还是计算型的属性。

- 如果你在重写属性中提供了 setter，那么你也一定要提供 getter。
- 如果你不想在重写版本中的 getter 里修改继承来的属性值，你可以直接通过super.someProperty来返回继承来的值，其中someProperty是你要重写的属性的名字。

```swift
class Circle {
    var radius = 12.5
    var area: String {
        return "矩形半径 \(radius) "
    }
}

// 继承超类 Circle
class Rectangle: Circle {
    var print = 7
    override var area: String {
        return super.area + " ，但现在被重写为 \(print)"
    }
}

let rect = Rectangle()
rect.radius = 25.0
rect.print = 3
print("Radius \(rect.area)")
```

子类可以在属性重写中为一个继承来的属性添加属性观察器。这样一来，当继承来的属性值发生改变时，就会监测到。

**注意：**不可以为继承来的常量存储型属性或继承来的只读计算型属性添加属性观察器。

```swift
class Circle {
    var radius = 12.5
    var area: String {
        return "矩形半径为 \(radius) "
    }
}

class Rectangle: Circle {
    var print = 7
    override var area: String {
        return super.area + " ，但现在被重写为 \(print)"
    }
}


let rect = Rectangle()
rect.radius = 25.0
rect.print = 3
print("半径: \(rect.area)")

class Square: Rectangle {
    override var radius: Double {
        didSet {
            print = Int(radius/5.0)+1
        }
    }
}


let sq = Square()
sq.radius = 100.0
print("半径: \(sq.area)")
```

# 十四、自动引用计数（ARC）

Swift 使用自动引用计数（ARC）这一机制来跟踪和管理应用程序的内存通常情况下我们不需要去手动释放内存，因为 ARC 会在类的实例不再被使用时，自动释放其占用的内存。

***ARC 功能***

- 当每次使用 init() 方法创建一个类的新的实例的时候，ARC 会分配一大块内存用来储存实例的信息。
- 内存中会包含实例的类型信息，以及这个实例所有相关属性的值。
- 当实例不再被使用时，ARC 释放实例所占用的内存，并让释放的内存能挪作他用。
- 为了确保使用中的实例不会被销毁，ARC 会跟踪和计算每一个实例正在被多少属性，常量和变量所引用。
- 实例赋值给属性、常量或变量，它们都会创建此实例的强引用，只要强引用还在，实例是不允许被销毁的。

```swift
class Person {
    let name: String
    init(name: String) {
        self.name = name
        print("\(name) 开始初始化")
    }
    deinit {
        print("\(name) 被析构")
    }
}

// 值会被自动初始化为nil，目前还不会引用到Person类的实例
var reference1: Person?
var reference2: Person?
var reference3: Person?

// 创建Person类的新实例
reference1 = Person(name: "Runoob")


//赋值给其他两个变量，该实例又会多出两个强引用
reference2 = reference1
reference3 = reference1

//断开第一个强引用
reference1 = nil
//断开第二个强引用
reference2 = nil
//断开第三个强引用，并调用析构函数
reference3 = nil
```

## 循环强引用

### 类实例之间的循环强引用

可能会写出这样的代码，一个类永远不会有0个强引用。这种情况发生在两个类实例互相保持对方的强引用，并让对方不被销毁。这就是所谓的循环强引用。

```swift
class Person {
    let name: String
    init(name: String) { self.name = name }
    var apartment: Apartment?
    deinit { print("\(name) 被析构") }
}

class Apartment {
    let number: Int
    init(number: Int) { self.number = number }
    var tenant: Person?
    deinit { print("Apartment #\(number) 被析构") }
}

// 两个变量都被初始化为nil
var runoob: Person?
var number73: Apartment?

// 赋值
runoob = Person(name: "Runoob")
number73 = Apartment(number: 73)

// 意感叹号是用来展开和访问可选变量 runoob 和 number73 中的实例
// 循环强引用被创建
runoob!.apartment = number73
number73!.tenant = runoob

// 断开 runoob 和 number73 变量所持有的强引用时，引用计数并不会降为 0，实例也不会被 ARC 销毁
// 注意，当你把这两个变量设为nil时，没有任何一个析构函数被调用。
// 强引用循环阻止了Person和Apartment类实例的销毁，并在你的应用程序中造成了内存泄漏
runoob = nil
number73 = nil
```



Swift 提供了两种办法用来解决你在使用类的属性时所遇到的循环强引用问题：

- 弱引用`weak`

  ```swift
  class Module {
      let name: String
      init(name: String) { self.name = name }
      var sub: SubModule?
      deinit { print("\(name) 主模块") }
  }
  
  class SubModule {
      let number: Int
      
      init(number: Int) { self.number = number }
      
      weak var topic: Module?
      
      deinit { print("子模块 topic 数为 \(number)") }
  }
  
  var toc: Module?
  var list: SubModule?
  toc = Module(name: "ARC")
  list = SubModule(number: 4)
  toc!.sub = list
  list!.topic = toc
  
  toc = nil
  list = nil
  ```

  

- 无主引用`unowned`

  ```swift
  class Student {
      let name: String
      var section: Marks?
      
      init(name: String) {
          self.name = name
      }
      
      deinit { print("\(name)") }
  }
  class Marks {
      let marks: Int
      unowned let stname: Student
      
      init(marks: Int, stname: Student) {
          self.marks = marks
          self.stname = stname
      }
      
      deinit { print("学生的分数为 \(marks)") }
  }
  
  var module: Student?
  module = Student(name: "ARC")
  module!.section = Marks(marks: 98, stname: module!)
  module = nil
  ```

弱引用和无主引用允许循环引用中的一个实例引用另外一个实例而不保持强引用。这样实例能够互相引用而不产生循环强引用。对于生命周期中会变为nil的实例使用弱引用。相反的，对于初始化赋值后再也不会被赋值为nil的实例，使用无主引用。

### 闭包引起的循环强引用

循环强引用还会发生在当你将一个闭包赋值给类实例的某个属性，并且这个闭包体中又使用了实例。这个闭包体中可能访问了实例的某个属性，例如self.someProperty，或者闭包中调用了实例的某个方法，例如self.someMethod。这两种情况都导致了闭包 "捕获" self，从而产生了循环强引用。

```swift
class HTMLElement {
    
    let name: String
    let text: String?
    
    lazy var asHTML: () -> String = {
        if let text = self.text {
            return "<\(self.name)>\(text)</\(self.name)>"
        } else {
            return "<\(self.name) />"
        }
    }
    
    init(name: String, text: String? = nil) {
        self.name = name
        self.text = text
    }
    
    deinit {
        print("\(name) is being deinitialized")
    }
    
}

// 创建实例并打印信息
var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello, world")
print(paragraph!.asHTML())
```

***当闭包和捕获的实例总是互相引用时并且总是同时销毁时，将闭包内的捕获定义为无主引用。相反的，当捕获引用有时可能会是nil时，将闭包内的捕获定义为弱引用。如果捕获的引用绝对不会置为nil，应该用无主引用，而不是弱引用。***

```swift
class HTMLElement {
    
    let name: String
    let text: String?
    
    lazy var asHTML: () -> String = {
        [unowned self] in
        if let text = self.text {
            return "<\(self.name)>\(text)</\(self.name)>"
        } else {
            return "<\(self.name) />"
        }
    }
    
    init(name: String, text: String? = nil) {
        self.name = name
        self.text = text
    }
    
    deinit {
        print("\(name) 被析构")
    }
    
}

//创建并打印HTMLElement实例
var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello, world")
print(paragraph!.asHTML())

// HTMLElement实例将会被销毁，并能看到它的析构函数打印出的消息
paragraph = nil
```

# 十五、协议

协议规定了用来实现某一特定功能所必需的方法和属性。任意能够满足协议要求的类型被称为遵循(conform)这个协议。类、结构体或枚举类型都可以遵循协议，并提供具体实现来完成协议定义的方法和功能。

定义协议：

```swift
protocol SomeProtocol {
    // 协议内容
}
```

要使类、结构体或枚举遵循某个协议，需要在类型名称后加上协议名称，中间以冒号:分隔，作为类型定义的一部分。***遵循多个协议时，各协议之间用逗号,分隔。***

```swift
struct SomeStructure: FirstProtocol, AnotherProtocol {
    // 结构体内容
}
class SomeClass: SomeSuperClass, FirstProtocol, AnotherProtocol {
    // 类的内容
}
```

尽管协议本身并不实现任何功能，但是协议可以被当做类型来使用。协议可以像其他普通类型一样使用，使用场景:

- 作为函数、方法或构造器中的参数类型或返回值类型
- 作为常量、变量或属性的类型
- 作为数组、字典或其他容器中的元素类型

## 1.属性定义

协议用于指定特定的实例属性或类属性，而不用指定是存储型属性或计算型属性。此外还必须指明是只读的还是可读可写的。协议中的通常用var来声明变量属性，在类型声明后加上{ set get }来表示属性是可读可写的，只读属性则用{ get }来表示。

```swift
protocol classa {
    
    var marks: Int { get set }
    var result: Bool { get }
    
    func attendance() -> String
    func markssecured() -> String
    
}

protocol classb: classa {
    
    var present: Bool { get set }
    var subject: String { get set }
    var stname: String { get set }
    
}

class classc: classb {
    var marks = 96
    let result = true
    var present = false
    var subject = "Swift 协议"
    var stname = "Protocols"
    
    func attendance() -> String {
        return "The \(stname) has secured 99% attendance"
    }
    
    func markssecured() -> String {
        return "\(stname) has scored \(marks)"
    }
}

```



## 2.定义`mutating`方法

有时需要在方法中改变它的实例，将mutating关键字作为函数的前缀，写在func之前，表示可以在该方法中修改它所属的实例及其实例属性的值。

```swift
protocol daysofaweek {
    mutating func show()
}

enum days: daysofaweek {
    case sun, mon, tue, wed, thurs, fri, sat
    mutating func show() {
        switch self {
        case .sun:
            self = .sun
            print("Sunday")
        case .mon:
            self = .mon
            print("Monday")
        case .tue:
            self = .tue
            print("Tuesday")
        case .wed:
            self = .wed
            print("Wednesday")
        case .thurs:
            self = .thurs
            print("Wednesday")
        case .fri:
            self = .fri
            print("Firday")
        case .sat:
            self = .sat
            print("Saturday")
        default:
            print("NO Such Day")
        }
    }
}

var res = days.wed
res.show()
```



## 3.定义构造方法

协议可以要求它的遵循者实现指定的构造器。在协议的定义里写下构造器的声明，但不需要写花括号和构造器的实体。

```swift
protocol tcpprotocol {
   init(aprot: Int)
}
```

在遵循该协议的类中实现构造器，并指定其为类的指定构造器或者便利构造器。在这两种情况下，你都必须给构造器实现标上"required"修饰符。使用required修饰符可以保证：所有的遵循该协议的子类，同样能为构造器规定提供一个显式的实现或继承实现。如果一个子类重写了父类的指定构造器，并且该构造器遵循了某个协议的规定，那么该构造器的实现需要被同时标示required和override修饰符。

```swift
protocol tcpprotocol {
   init(aprot: Int)
}

class tcpClass: tcpprotocol {
   required init(aprot: Int) {
   }
}
```

```swift
protocol tcpprotocol {
    init(no1: Int)
}

class mainClass {
    var no1: Int // 局部变量
    init(no1: Int) {
        self.no1 = no1 // 初始化
    }
}

class subClass: mainClass, tcpprotocol {
    var no2: Int
    init(no1: Int, no2 : Int) {
        self.no2 = no2
        super.init(no1:no1)
    }
    // 因为遵循协议，需要加上"required"; 因为继承自父类，需要加上"override"
    required override convenience init(no1: Int)  {
        self.init(no1:no1, no2:0)
    }
}
```

## 4.协议的继承

协议能够继承一个或多个其他协议，可以在继承的协议基础上增加新的内容要求。协议的继承语法与类的继承相似，多个被继承的协议间用逗号分隔：

```swift
protocol InheritingProtocol: SomeProtocol, AnotherProtocol {
    // 协议定义
}
```

## 5.类专属协议

在协议的继承列表中,通过添加class关键字,限制协议只能适配到类（class）类型。

```swift
protocol SomeClassOnlyProtocol: class, SomeInheritedProtocol {
    // 协议定义
}
```

## 6.协议合成

Swift支持合成多个协议，这在我们需要同时遵循多个协议时非常有用。使用`&`符号合成遵循将多个协议类型。

```swift
protocol Stname {
    var name: String { get }
}

protocol Stage {
    var age: Int { get }
}

struct Person: Stname, Stage {
    var name: String
    var age: Int
}

func show(celebrator: Stname & Stage) {
    print("\(celebrator.name) is \(celebrator.age) years old")
}
```

## 7.验证是否遵循了协议

可以使用is和as操作符来检查是否遵循某一协议或强制转化为某一类型。

- `is`操作符用来检查实例是否遵循了某个协议。
- `as?`返回一个可选值，当实例遵循协议时，返回该协议类型;否则返回`nil`。
- `as!`用以强制向下转型，如果强转失败，会引起运行时错误。

```swift
protocol HasArea {
    var area: Double { get }
}

// 定义了Circle类，都遵循了HasArea协议
class Circle: HasArea {
    let pi = 3.1415927
    var radius: Double
    var area: Double { return pi * radius * radius }
    init(radius: Double) { self.radius = radius }
}

// 定义了Country类，都遵循了HasArea协议
class Country: HasArea {
    var area: Double
    init(area: Double) { self.area = area }
}

// Animal是一个没有实现HasArea协议的类
class Animal {
    var legs: Int
    init(legs: Int) { self.legs = legs }
}

let objects: [AnyObject] = [
    Circle(radius: 2.0),
    Country(area: 243_610),
    Animal(legs: 4)
]

for object in objects {
    // 对迭代出的每一个元素进行检查，看它是否遵循了HasArea协议
    if let objectWithArea = object as? HasArea {
        print("面积为 \(objectWithArea.area)")
    } else {
        print("没有面积")
    }
}
```



# 十六、泛型

Swift 提供了泛型让你写出灵活且可重用的函数和类型。泛型使用了占位类型名（在这里用字母 T 来表示）来代替实际类型名。

```swift
func swapTwoValues<T>(_ a: inout T, _ b: inout T)
```

swapTwoValues 后面跟着占位类型名（T），并用尖括号括起来（`<T>`）。这个尖括号告诉 Swift 那个 T 是 swapTwoValues(_:_:) 函数定义内的一个占位类型名，因此 Swift 不会去查找名为 T 的实际类型。

```swift
// 定义一个交换两个变量的函数
func swapTwoValues<T>(_ a: inout T, _ b: inout T) {
    let temporaryA = a
    a = b
    b = temporaryA
}
 
var numb1 = 100
var numb2 = 200
 
print("交换前数据:  \(numb1) 和 \(numb2)")
swapTwoValues(&numb1, &numb2)
print("交换后数据: \(numb1) 和 \(numb2)")
 
var str1 = "A"
var str2 = "B"
 
print("交换前数据:  \(str1) 和 \(str2)")
swapTwoValues(&str1, &str2)
print("交换后数据: \(str1) 和 \(str2)")
```

Swift 允许你定义你自己的泛型类型。自定义类、结构体和枚举作用于任何类型，如同 Array 和 Dictionary 的用法。

```swift
//泛型栈
struct Stack<Element> {
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
 
var stackOfStrings = Stack<String>()
print("字符串元素入栈: ")
stackOfStrings.push("google")
stackOfStrings.push("runoob")
print(stackOfStrings.items);
 
let deletetos = stackOfStrings.pop()
print("出栈元素: " + deletetos)
 
var stackOfInts = Stack<Int>()
print("整数元素入栈: ")
stackOfInts.push(1)
stackOfInts.push(2)
print(stackOfInts.items);
```

## 1.类型约束

类型约束指定了一个必须继承自指定类的类型参数，或者遵循一个特定的协议或协议构成。一个在一个类型参数名后面的类型约束，通过冒号分割，来作为类型参数链的一部分。这种作用于泛型函数的类型约束的基础语法如下所示（和泛型类型的语法相同）：

```swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // 这里是泛型函数的函数体部分
}
```

第一个类型参数 T，有一个要求 T 必须是 SomeClass 子类的类型约束；第二个类型参数 U，有一个要求 U 必须符合 SomeProtocol 协议的类型约束。



## 2.关联类型

Swift 中使用 associatedtype 关键字来设置关联类型实例。

```swift
// Container 协议
protocol Container {
    associatedtype ItemType
    // 添加一个新元素到容器里
    mutating func append(_ item: ItemType)
    // 获取容器中元素的数
    var count: Int { get }
    // 通过索引值类型为 Int 的下标检索到容器中的每一个元素
    subscript(i: Int) -> ItemType { get }
}

// Stack 结构体遵从 Container 协议
struct Stack<Element>: Container {
    // Stack<Element> 的原始实现部分
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
    // Container 协议的实现部分
    mutating func append(_ item: Element) {
        self.push(item)
    }
    var count: Int {
        return items.count
    }
    subscript(i: Int) -> Element {
        return items[i]
    }
}

var tos = Stack<String>()
tos.push("google")
tos.push("runoob")
tos.push("taobao")
// 元素列表
print(tos.items)
// 元素个数
print( tos.count)
```



## 3.`where`语句

where语句，紧跟在在类型参数列表后面，where语句后跟一个或者多个针对关联类型的约束，以及（或）一个或多个类型和关联类型间的等价(equality)关系。

```swift
// Container 协议
protocol Container {
    associatedtype ItemType
    // 添加一个新元素到容器里
    mutating func append(_ item: ItemType)
    // 获取容器中元素的数
    var count: Int { get }
    // 通过索引值类型为 Int 的下标检索到容器中的每一个元素
    subscript(i: Int) -> ItemType { get }
}
 
// // 遵循Container协议的泛型TOS类型
struct Stack<Element>: Container {
    // Stack<Element> 的原始实现部分
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
    // Container 协议的实现部分
    mutating func append(_ item: Element) {
        self.push(item)
    }
    var count: Int {
        return items.count
    }
    subscript(i: Int) -> Element {
        return items[i]
    }
}
// 扩展，将 Array 当作 Container 来使用
extension Array: Container {}
 
func allItemsMatch<C1: Container, C2: Container>
    (_ someContainer: C1, _ anotherContainer: C2) -> Bool
    where C1.ItemType == C2.ItemType, C1.ItemType: Equatable {
        
        // 检查两个容器含有相同数量的元素
        if someContainer.count != anotherContainer.count {
            return false
        }
        
        // 检查每一对元素是否相等
        for i in 0..<someContainer.count {
            if someContainer[i] != anotherContainer[i] {
                return false
            }
        }
        
        // 所有元素都匹配，返回 true
        return true
}
var tos = Stack<String>()
tos.push("google")
tos.push("runoob")
tos.push("taobao")
 
var aos = ["google", "runoob", "taobao"]
 
if allItemsMatch(tos, aos) {
    print("匹配所有元素")
} else {
    print("元素不匹配")
}
```

# 十七、访问控制

访问控制可以限定其他源文件或模块中代码对你代码的访问级别。可以明确地给单个类型（类、结构体、枚举）设置访问级别，也可以给这些类型的属性、函数、初始化方法、基本类型、下标索引等设置访问级别。协议也可以被限定在一定的范围内使用，包括协议里的全局常量、变量和函数。

## 1.访问级别

Swift 为代码中的实体提供了四种不同的访问级别，按级别从高到低排序：**public、internal、fileprivate、private**。

| 访问级别    | 定义                                                         |
| :---------- | :----------------------------------------------------------- |
| `Open`      | 所修饰的属性或方法在源代码所在的整个模块都可以访问。只能作用于类和类的成员，可以被任何人使用，包括重写和继承 |
| public      | 可以被任何人使用。但其他模块中不可以被重写和继承，而在本模块内可以被重写和继承 |
| internal    | 所修饰的属性或方法在源代码所在的整个模块都可以访问。如果是框架或者库代码，则在整个框架内部都可以访问，框架由外部代码所引用时，则不可以访问。如果是App代码，也是在整个App代码，也是在整个App内部可以访问（默认） |
| fileprivate | 文件内私有，只能在当前源文件中使用。                         |
| private     | 所修饰的属性或者方法只能在当前类里访问                       |



模块指的是以独立单元构建和发布的 Framework 或 Application。在 Swift 中的一个模块可以使用 `import` 关键字引入另外一个模块。源文件是单个源码文件，它通常属于一个模块， 源文件可以包含多个类和函数 的定义。

***未指定访问级别默认为 `internal`***

## 2.不同类型访问级别的原则

### 2.1元组

元组的访问级别与元组中访问级别最低的类型一致。

### 2.2函数

函数的访问级别需要根据该函数的参数类型和返回类型的访问级别得出。如果函数返回类型的访问级别是 private，那么必须使用 private 修饰符，明确的声明该函数。

```swift
private func someFunction() -> (SomeInternalClass, SomePrivateClass) {
    // 函数实现
}
```



### 2.3枚举

枚举中成员的访问级别继承自该枚举，你不能为枚举中的成员单独申明不同的访问级别。

```swift
public enum Student {
    case Name(String)
    case Mark(Int,Int,Int)
}
```



### 2.4子类

子类的访问级别不得高于父类的访问级别。

```swift
public class SuperClass {
    fileprivate func show() {
        print("超类")
    }
}
 
// 访问级别不能高于超类 public > internal
internal class SubClass: SuperClass  {
    override internal func show() {
        print("子类")
    }
}
```



### 2.5常量、变量、属性、下标

常量、变量、属性不能拥有比它们的类型更高的访问级别。如果常量、变量、属性、下标索引的定义类型是private级别的，那么它们必须要明确的申明访问级别为private:

```swift
private var privateInstance = SomePrivateClass()
```



### 2.6Getter和Setter

常量、变量、属性、下标索引的Getters和Setters的访问级别继承自它们所属成员的访问级别。Setter的访问级别可以低于对应的Getter的访问级别，这样就可以控制变量、属性或下标索引的读写权限。

```swift
class Samplepgm {
    fileprivate var counter: Int = 0{
        willSet(newTotal){
            print("计数器: \(newTotal)")
        }
        didSet{
            if counter > oldValue {
                print("新增加数量 \(counter - oldValue)")
            }
        }
    }
}
 
let NewCounter = Samplepgm()
NewCounter.counter = 100
NewCounter.counter = 800
```



### 2.7构造器

我们可以给自定义的初始化方法申明访问级别，但是要不高于它所属类的访问级别。但必要构造器例外，它的访问级别必须和所属类的访问级别相同。如同函数或方法参数，初始化方法参数的访问级别也不能低于初始化方法的访问级别。

Swift为结构体、类都提供了一个默认的无参初始化方法，用于给它们的所有属性提供赋值操作，但不会给出具体值。默认初始化方法的访问级别与所属类型的访问级别相同。



### 2.8协议

如果想为一个协议明确的申明访问级别，那么需要注意一点，就是你要确保该协议只在你申明的访问级别作用域中使用。如果你定义了一个public访问级别的协议，那么实现该协议提供的必要函数也会是public的访问级别。

### 2.9扩展

扩展成员应该具有和原始类成员一致的访问级别。

### 2.10泛型

泛型类型或泛型函数的访问级别取泛型类型、函数本身、泛型类型参数三者中的最低访问级别。

### 2.11类型别名

一个类型别名的访问级别不可高于原类型的访问级别。

# 十八、可选链

可选链（Optional Chaining）是一种可以请求和调用属性、方法和子脚本的过程，用于请求或调用的目标可能为nil。

可选链返回值：

- 如果目标有值，调用就会成功，返回该值，如果没有返回值则返回`Void`
- 如果目标为nil，调用将返回nil

通过在属性、方法、或下标脚本的可选值后面放一个问号(?)，即可定义一个可选链。多次请求或调用可以被链接成一个链，如果任意一个节点为nil将导致整条链失效。

| 可选链 '?'                                 | 感叹号（!）强制展开方法，属性，下标脚本可选链          |
| ------------------------------------------ | ------------------------------------------------------ |
| ? 放置于可选值后来调用方法，属性，下标脚本 | ! 放置于可选值后来调用方法，属性，下标脚本来强制展开值 |
| 当可选为 nil 输出比较友好的错误信息        | 当可选为 nil 时强制展开执行错误                        |

```swift
class Person {
    var residence: Residence?
}

class Residence {
    var numberOfRooms = 1
}

let john = Person()

// 链接可选residence?属性，如果residence存在则取回numberOfRooms的值
if let roomCount = john.residence?.numberOfRooms {
    print("John 的房间号为 \(roomCount)。")
} else {
    print("不能查看房间号")
}
```

# 十九、扩展

通过扩展来扩充已存在类型( 类，结构体，枚举等)。扩展可以为已存在的类型添加属性，方法，下标脚本，协议等成员。扩展声明使用关键字`extension`。

```swift
extension SomeType {
    // 加到SomeType的新功能写到这里
}
extension SomeType: SomeProtocol, AnotherProctocol {
    // 协议实现写到这里
}
```

Swift 中的扩展可以：

- 添加计算型属性和计算型静态属性
- 定义实例方法和类型方法
- 提供新的构造器
- 定义下标
- 定义和使用新的嵌套类型
- 使一个已有类型符合某个协议
- 扩展一个协议，为可选方法提供实现

当你扩展一个泛型类型的时候（使用 extension 关键字），你并不需要在扩展的定义中提供类型参数列表。更加方便的是，原始类型定义中声明的类型参数列表在扩展里是可以使用的，并且这些来自原始类型中的参数名称会被用作原始定义中类型参数的引用。

```swift
struct Stack<Element> {
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
 
extension Stack {
    var topItem: Element? {
       return items.isEmpty ? nil : items[items.count - 1]
    }
}
 
var stackOfStrings = Stack<String>()
print("字符串元素入栈: ")
stackOfStrings.push("google")
stackOfStrings.push("runoob")
 
if let topItem = stackOfStrings.topItem {
    print("栈中的顶部元素是：\(topItem).")
}
 
print(stackOfStrings.items)
```

```swift
protocol OptionalProtocol {
    func optionalMethod()        // 可选
    func necessaryMethod()       // 必须
    func anotherOptionalMethod() // 可选
}

extension OptionalProtocol {
    func optionalMethod() {
        print("Implemented in extension")
    }

    func anotherOptionalMethod() {
        print("Implemented in extension")
    }
}

class MyClass: OptionalProtocol {
    func necessaryMethod() {
        print("Implemented in Class3")
    }

    func optionalMethod() {
        print("Implemented in Class3")
    }
}

let obj = MyClass()
obj.necessaryMethod() // Implemented in Class3
obj.optionalMethod()  // Implemented in Class3
obj.anotherOptionalMethod() // Implemented in extension
```



# 二十、类型转换

Swift 中类型转换使用 is 和 as 操作符实现，is 用于检测值的类型，as 用于转换类型。类型转换也可以用来检查一个类是否实现了某个协议。

## 1.检查类型

类型检查使用 `is` 关键字。检查一个实例是否属于特定子类型。若实例属于那个子类型，类型检查操作符返回 true，否则返回 false。

```swift
if item is Chemistry {
  //statements
} 
```



## 2.向下转型

向下转型，用类型转换操作符(`as?` 或 `as!`)当你不确定向下转型可以成功时，用类型转换的条件形式(`as?`)。条件形式的类型转换总是返回一个可选值（optional value），并且若下转是不可能的，可选值将是 `nil`。只有你可以确定向下转型一定会成功时，才使用强制形式(as!)。当你试图向下转型为一个不正确的类型时，强制形式的类型转换会触发一个运行时错误。

```swift
// 类型转换的条件形式
if let show = item as? Chemistry {
	//statements      
}

```



## 3.`Any`和`AnyObject`

Swift为不确定类型提供了两种特殊类型别名：

- `AnyObject`可以代表任何class类型的实例。
- `Any`可以表示任何类型，包括方法类型（function types）

```swift
// 可以存储Any类型的数组 exampleany
var exampleany = [Any]()
```

```swift
// [AnyObject] 类型的数组
let saprint: [AnyObject] = [
    Chemistry(physics: "固体物理", equations: "赫兹"),
    Maths(physics: "流体动力学", formulae: "千兆赫"),
    Chemistry(physics: "热物理学", equations: "分贝"),
    Maths(physics: "天体物理学", formulae: "兆赫"),
    Maths(physics: "微分方程", formulae: "余弦级数")]
```

