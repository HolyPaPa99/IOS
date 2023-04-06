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

# 十一、闭包





# 十二、枚举





# 十三、结构体





# 十四、类







# 十五、继承





# 十六、自动引用计数（ARC）





# 十七、协议





# 十八、泛型





