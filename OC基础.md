# 一、命名规则

名称必须以字母或下划线开头，之后可以是任何字母、下划线或0～9之间的数字组合。Object-C中是区分大小写的。

# 二、类

## 1.类的组成

类由类声明和类实现两个部分组成。

类声明放在"类名.h"头文件中，一般格式如下：

```objective-c
@interface NewClassName: ParentClassName
  //property and method declarations
  
@end
```

类实现存放在"类名.m"文件中，一般格式如下：

```objective-c
@implementation NewClassName
{
  //member declarations
}
//method definitions
@end
```



## 2.类方法声明

类方法的声明：

```objective-c
- (void) setNumerator: (int) n;
```

方法类型	返回类型	方法名称: 参数类型	参数名称;

其中方法类型：

* 负号`-`  表示该方法是一个实例方法
* 正号`+` 表示该方法是一个类方法

如果具有多个参数，其声明方式如下：

```objective-c
- (void) setTo: (int) n over: (int) d;
```

还可以不带参数名：

```objective-c
- (void) setTo: (int) n : (int) d;
```



## 3.数据封装

类实例变量对外部是隐藏的不能被直接访问。可使用`@property`和`@synthesize`来合成存取方法，供外部调用。例如：

```objective-c
@interface Fraction: NSObject
  @property int numerator, denominator;
	- (void) print;
	- (double) convertToNum;
@end
```

```objective-c
#import "Fraction.h"
@implementation Fraction
	@synthesize numerator, denominator;
	//method definitions
@end
```



## 4.类的实例化

类对象的声明如下：

```objective-c
Fraction *myFraction;
```

其中`*`号表示`myFraction`是Fraction类对象的引用（指针）。

类实例的初始化：

```objective-c
Fraction *myFraction;//声明定义
myFraction = [Fraction alloc];//分配内存
myFraction = [Fraction init];//初始化
```

等价于：

```
Fraction *myFraction = [[Fraction alloc] init];
```

等价于：

```objective-c
Fraction *myFraction = [Fraction new];
```



## 5.类属性的访问及方法调用

* 类属性访问和赋值

  ```objective-c
  //属性访问
  instance.property
  ```

  ```objective-c
  //赋值
  instance.property = value;
  //或者
  [instance setProperty: value];
  ```

  

* 方法调用

  ```objective-c
  [类名/实例名 方法名: 参数];
  ```

  例如：

  ```objective-c
  -(void) setTo: (int)n over:(int) d;
  ```

  ```objective-c
  //调用
  [myFraction setTo: 100 over: 200];
  ```

  

  ```objective-c
  //不带参数名的方式
  -（void) setTo: (int)n : (int)d;
  ```

  ```objective-c
  //调用
  [myFraction setTo: 100 : 200];
  ```

# 二、`static`关键字

在变量声明前加上`static`关键字，可以使局部变量保留多次调用一个方法所得的值。它们只在程序执行时初始化一次，并且在多次调用方法时保存这些数值。例如：

```objective-c
-(int) showPage
{
  static int pageCount = 0;
  //statements
  ++ pageCount;
  //other statements
  return pageCount;
}
```

可以将变量的声明移到所有方法声明的外部，通常放在`implementation`文件的开始处。这样所有地的方法都可以访问它们。例如：

```objective-c
#import "Printer.h"
static int pageCount;
@implementation Printer
  -(int) showPage
	{
  	//statements
  	++ pageCount;
  	//statements
  	return pageCount;
	}
@end
```

# 三、`self`关键字

`self`关键字是用来指明对象是当前方法的接收者。





