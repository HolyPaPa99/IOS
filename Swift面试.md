## 1.Swift的优点

`Swift`是苹果在2014年6月WWDC发布的全新编程语言，优点：

* 类型安全
* 语法和文件结构简化
* 性能高



## 2.Swift和OC混编

Swift 调用 OC代码
 需要创建一个 `Target-BriBridging-Header.h` 的桥文件,在乔文件导入需要调用的OC代码头文件即可

OC 调用 Swift代码
 直接导入 `Target-Swift.h`文件即可, Swift如果需要被OC调用,需要使用@objc 对方法或者属性进行修饰



## 3.class和struct的区别

在 Swift 中,class 是引用类型(指针类型), struct 是值类型。值类型在传递和赋值时将进行复制，引用类型只会使用引用对象的一个"指向"。

class的优点：

* class可以继承而struct不可以

* class可以在运行时检查和解释一个实例对象

* class可以用 deinit来释放资源

* 一个class类可以被多次引用

  

struct的优点：

* 结构较小,适用于复制操作
* 更安全，无需担心内存泄露问题



## 4.可选型（Optional）

如果要声明一个变量或属性可能为空`nil`，那么可以在类型名称后加上`?`或使用`Optional`关键字`Optional(类型名称)`来定义一个可选型，数值类型和引用类型都可以是可选型。



## 5.泛型

泛型是为了提高代码的灵活性和可重用性。泛型可以把类型参数化，从而提高代码的可复用性。



## 6.访问控制

Swift提供5个级别的访问控制权限,从高到低依次是 `open, public, internal, fileprivate, private`。

* **open**: 具备最高访问权限,其修饰的类可以和方法,可以在任意 模块中被访问和重写.

* **public**: 权限仅次于 open，和 open 唯一的区别是: 不允许其他模块进行继承、重写

* **internal**: 默认权限, 只允许在当前的模块中访问，可以继承和重写,不允许在其他模块中访问

* **fileprivate**: 修饰的对象只允许在当前的文件中访问;

* **private**: 最低级别访问权限,只允许在定义的作用域内访问



## 7.`strong`、`weak`和`unowned`

Swift 的内存管理机制同OC一致,都是ARC管理机制。一般引用变量或属性默认都是强引用`strong`，这样一旦出现循环强引用对象就无法被ARC销毁释放资源。因此Swift提供了`weak`弱引用和`unowned`无主引用来解决这种问题。

***对于生命周期中会变为nil的实例使用弱引用。相反的，对于初始化赋值后再也不会被赋值为nil的实例，使用无主引用。***



## 8.copy-on-write

当你有一个占用内存很大的一个值类型，并且不得不将它赋值给另一个变量或者当做函数的参数传递的时候，拷贝它的值是一个非常消耗内存的操作，因为你不得不拷贝它所有的东西放置在另一块内存中。

为了优化这个问题，Swift 对于一些特定的值类型做了一些优化，在对于 Array 进行拷贝的时候，当传递的值进行改变的时候才会发生真正的拷贝。而对于String、Int 等值类型，在赋值的时候就会发生拷贝。

* Copy-on-Write 是一种用来优化占用内存大的值类型的拷贝操作的机制。
* 对于 Int、String 等基本类型的值类型，它们在赋值的时候就会发生拷贝，它们没有 Copy-on-Write 这一特性（因为Copy-on-Write带来的开销往往比直接复制的开销要大）。
* 对于 Array类型，当它们赋值的时候不会发生拷贝，只有在修改的之后才会发生拷贝，即 Copy-on-Write。
* 对于自定义的结构体在赋值的时候就会发生拷贝，不支持 Copy-on-Write。

```swift
import Foundation

func address(_ o: UnsafeRawPointer)->String {
    let address = String.init(format: "%018p", Int(bitPattern: o))
    return address
}

//整型
print("整型")
var int1: Int = 1
address(&int1)
var int2 = int1
address(&int2)
int2 = 3
address(&int2)
//浮点
print("浮点")
var flo1: Float = 0.1
address(&flo1)
var flo2 = flo1
address(&flo2)
flo2 = 0.2
address(&flo2)


//布尔
print("布尔")
var bo1: Bool = false
address(&bo1)
var bo2 = bo1
address(&bo2)
bo2 = true
address(&bo2)


//字符
print("字符")
var cha1: Character = "a"
address(&cha1)
var cha2 = cha1
address(&cha2)
cha2 = "b"
address(&cha2)



//结构
struct Person{
    var name: String
}
print("结构struct")
var p1: Person = Person(name: "Jadon")
address(&p1)
var p2 = p1
address(&p2)
p2.name = "James"
address(&p2)
print(p1.name)

//枚举
enum E{
    case E1,E2,E3
}
print("枚举")
var e1: E = .E1
address(&e1)
var e2 = e1
address(&e2)
e2 = .E2
address(&e2)

//数组
print("数组")
var arr1: [Int] = [1,2,3,4]
address(&arr1)
var arr2 = arr1
address(&arr2)
arr2.append(5)
address(&arr2)

//元组
print("元组")
var tu1 = (10, "tu1")
address(&tu1)
var tu2 = tu1
address(&tu2)
tu2 = (20, "tu2")
address(&tu2)


//字典
print("字典")
var d1 = ["d1": 10]
address(&d1)
var d2 = d1
address(&d2)
d2["d1"] = 20
address(&d2)


//集合
print("集合")
var set1: Set = [1,2,3,4,5,6,7]
address(&set1)
var set2 = set1
address(&set2)
set2.insert(8)
address(&set2)


//字符串
print("字符串")
var str1: String = "str1"
address(&str1)
var str2 = str1
address(&str2)
str2 = "str2"
address(&str2)
print(str1)

//类
class Animal {
    var name: String
    init(name: String){
        self.name = name
    }
}
print("类")
var an1: Animal = Animal(name:"cat")
address(&an1)
var an2 = an1
address(&an2)
an2.name = "dog"
address(&an2)
an1.name
```

经过以上测试发现只有`Array`数组类型支持`Copy-On-Write`优化机制。

## 9.属性观察器

属性观察器监控和响应属性值的变化，每次属性被设置值的时候都会调用属性观察器，甚至新的值和现在的值相同的时候也不例外。可以为除了延迟存储属性之外的其他存储属性添加属性观察器，也可以通过重载属性的方式为继承的属性（包括存储属性和计算属性）添加属性观察器。可以为属性添加如下的一个或全部观察器：

- `willSet`在设置新的值之前调用
- `didSet`在新的值被设置之后立即调用
- willSet和didSet观察器在属性初始化过程中不会被调用

计算属性和属性观察器所描述的模式也可以用于全局变量和局部变量。

## 10.值类型优点

值类型和引用类型相比,最大优势可以高效的使用内存,值类型在栈上操作,引用类型在堆上操作,栈上操作仅仅是单个指针的移动,而堆上操作牵涉到合并,位移,重链接,Swift 这样设计减少了堆上内存分配和回收次数,使用 copy-on-write将值传递与复制开销降到最低

在Swift中Int、Float、Double、Bool、Character、String、Array、Set、Dictionary、枚举、struct都是值类型。



## 11.将`protocol`中的部分方法设计为可选

方式一：

在协议和方法前添加`@objc`，然后在方法面前添加`optional`关键字，将协议转成OC方式。

```swift
@objc protocol someProtocol {
  @objc optional fun test()
}
```

方式二：

使用`extension`定义部分方法的默认实现。

```swift
protocol someProtocol {
  func test()
}

extension someProtocol {
  func test() {
    print("test")
  }
}
```



## 12.Swift和OC初始化方法有什么不同

Swift的初始化方法更加严格和准确，Swift初始化方法需要保证所有地的非`optional`的成员变量都完成初始化，同时swift新增了`convenience`和`required`两个修饰初始化器的关键字。

* `convenience`只提供一种方便的初始化器，必须通过一个指定初始化器来完成初始化
* `required`是强制子类重写父类中所修饰的初始化方法



## 13.比较Swift和OC中`protocol`的不同之处

Swift和OC中`protocol`都可以被用作代理。Swift中的`protocol`还可以对接口进行抽象，应用面向协议编程从而大大提高效率。Swift中的`protocol`可以用于值类型：结构体和枚举。



## 14.Swift和OC中的自省（类型判断）

OC：

```objective-c
[obj isKindOfClass: [SomeClass class]];
[obj isMemberOfClass: [SomeClass class]];
```



Swift:

```swift
obj is SomeStruct
obj is SomeEnum
obj is SomeClass
obj is SomeProtocol
```

Swift使用`is`来判断是否属于某一类型。



## 15.重载

函数重载是指函数名称相同，但函数参数个数不同或参数类型不同或参数标签不同，返回值类型与函数重载无关。



## 16.Swift中枚举的关联值和原始值有什么不同

* 关联值

  有时会将枚举的成员值跟其他类型的变量关联存储在一起，这些变量值是在枚实例创建时传入的，是可变的。

  ```swift
  enum Date{
    case digit(year: Int, month: Int, day: Int)
    case string(String)
  }
  
  let today = Date.digit(year: 2023, month: 04, day: 12)
  let tomorrow = Date.string("2023-04-13")
  ```

  

* 原始值

  枚举成员可以使用相同类型的默认值，原始值是在定义枚举时被预先填充的值。对于一个特定的枚举成员，它的原始值始终不变。

  ```swift
  enum Animal: String{
    case Cat = "Cat"
    case Dog = "Dog"
  }
  ```

## 17.闭包

语法格式：

```swift
{(参数列表) -> 返回值类型 in
  //函数体代码
}
```

尾随闭包：

将一个很长的闭包表达式作为函数最后一个实参，增强代码的可读性。尾随闭包是一个被书写在函数调用括号后面的闭包表达式。

```swift
func someFunction(v1: Int, v2: Int, fn: (Int, Int)->Int) {
  print(fn(v1,v2))
}

//尾随闭包式调用
someFunction(v1: 10, v2: 20){
  $0 + $1
}
```



逃逸闭包：

当闭包作为一个实际参数传递给一个函数或者变量的时候，闭包有可能在函数结束后调用，闭包调用逃离了函数的作用域，需要通过@escaping声明。

```swift
class Closure{
    var handle: ((Int) -> Void)?

    init(_ handler: @escaping (Int) -> Void) {
        self.handle = handler
    }
}
```



自动闭包：

- 自动闭包是一种自动创建的闭包，用于包装传递给函数作为参数的表达式。
- 这种闭包不接受任何参数，当它被调用的时候，会返回被包装在其中的表达式的值。
- 这种便利语法让你能够省略闭包的花括号，用一个普通的表达式来代替显式的闭包。
- 自动闭包让你能够延迟求值，因为直到你调用这个闭包，代码段才会被执行。
- 延迟求值对于那些有副作用（Side Effect）和高计算成本的代码来说是很有益处的，因为它使得你能控制代码的执行时机。

```swift
func getFirstPositive(_ v1: Int, _ v2: @autoclosure () -> Int) -> Int? {
    return v1 > 0 ? v1 : v2()
}
getFirstPositive(10, 20)
```



## 18.存储属性和计算属性的区别

存储属性：

- 类似于成员变量这个概念
- 存储在实例对象的内存中
- 结构体、类可以定义存储属性
- 枚举不可以定义存储属性

计算属性：

- 本质就是方法(函数)
- 不占用实例对象的内存
- 枚举、结构体、类都可以定义计算属性

```swift
struct Circle {
    // 存储属性
    var radius: Double
    // 计算属性
    var diameter: Double {
        set {
            radius = newValue / 2
        }
        get {
            return radius * 2
        }
    }
}
```





## 19.延迟属性

延迟存储属性是指当第一次被调用的时候才会计算其初始值的属性。在属性声明前使用 **lazy** 来标示一个延迟存储属性。

必须将延迟存储属性声明成变量（使用*`var`*关键字），因为属性的值在实例构造完成之前可能无法得到。而常量属性在构造过程完成之前必须要有初始值，因此无法声明成延迟属性。

```swift
class PhotoView {
    // 延迟存储属性
    lazy var image: Image = {
        let url = "https://...x.png"        
        let data = Data(url: url)
        return Image(data: data)
    }() 
} 
```



## 20.类型属性

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



## 21.单例

```swift
public class FileManager {
    public static let shared = FileManager()
    private init() { }
}
```



## 22.下标

下标脚本可以定义在类（Class）、结构体（structure）和枚举（enumeration）这些目标中，可以认为是访问对象、集合或序列的快捷方式，不需要再调用实例的特定的赋值和访问方法。定义下标脚本使用`subscript`关键字，显式声明入参（一个或多个）和返回类型。与实例方法不同的是下标脚本可以设定为读写或只读。

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





## 23.可选链

可选链（Optional Chaining）是一种可以请求和调用属性、方法和子脚本的过程，用于请求或调用的目标可能为nil。通过在属性、方法、或下标脚本的可选值后面放一个问号(?)，即可定义一个可选链。多次请求或调用可以被链接成一个链，如果任意一个节点为nil将导致整条链失效。

- 如果目标有值，调用就会成功，返回该值，如果没有返回值则返回`Void`
- 如果目标为nil，调用将返回nil



## 24.运算符重载

类、结构体、枚举可以为现有的运算符提供自定义的实现，这个操作叫做:运算符重载。

```swift
struct Point {
    var x: Int
    var y: Int

    // 重载运算符
    static func + (p1: Point, p2: Point) -> Point   {
        return Point(x: p1.x + p2.x, y: p1.y + p2.y)
    }
}

var p1 = Point(x: 10, y: 10)
var p2 = Point(x: 20, y: 20)
var p3 = p1 + p2
```







