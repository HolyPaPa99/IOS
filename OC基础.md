# 一、命名规则

名称必须以字母或下划线开头，之后可以是任何字母、下划线或0～9之间的数字组合。Object-C中是区分大小写的。

# 二、数据类型

## 1.基础数据类型

| 类型                   | NSLog字符                   | 描述|
| ---------------------- | --------------------------- |   |
| char                   | %c                          |   |
| short int              | %hi、%hx、%ho               |   |
| unsigned short int     | %hu、%hx、%ho %hu、%hx、%ho |   |
| int                    | %i、%x、%o                  | 32/64位 |
| unsigned int           | %u、%x、%o                  |   |
| long int               | %li、%lx、%lo               |   |
| unsigned long int      | %lu、%lx、%lo               |   |
| long long int          | %lli、%llx、&llo            |   |
| unsigned long long int | %llu、%llx、%llo            |   |
| float | %f、%e、%g、%a |   |
| double | %f、%e、%g、%a |   |
| long double | %f、%e、%g、%a |   |
| id | %p | id数据类型可以存储任何类型的对象 |

## 2.对象引用类型

使用`*`号表示当前变量是指定类对象引用变量，例如：

```objective-c
Fraction *myFraction;
```



## 3.`id`类型

这是一种通用的对象类型，也就是说，`id`类型变量可用来存储任何类的实例对象。

```objective-c
id dataValue = [Fraction new];
```



## 4.枚举类型

枚举数据类型的定义以关键字`enum`开头，之后是枚举数据类型的名称，然后是标识符序列，例如：

```objective-c
enum flag 
{
  false, 
  true
};
```

如果希望一个枚举标识符对应一个特定的整数值，那么可以在定义数据类型时给该标识符指定整数值。

```objective-c
enum direction
{
  up,
  down,
  left=10,
  right
};
```

```objective-c
//枚举变量定义与赋值
enum direction ahead;
ahead = left;
```



## 5.`bool`/`BOOL`和`Boolean`值

`bool`表示布尔类型，`BOOL`是`bool`的类型符号。

```objective-c
//在objc/objc.h类中是这样定义BOOL类型的:
typedef bool BOOL;
```

Boolean value包括：

| YES  | 1    |
| ---- | ---- |
| NO   | 0    |



## 6.`typedef`指令

`typedef`指令用于为数据类型另外指派一个名称。例如：

```objective-c
typedef int Counter;
Counter j,n;
typedef enum {east, west, south, north} Direction;
Direction step1, step2;
```



# 三、运算表达式

## 1.算术运算符

| 算术运算符 | 语义   | 与赋值运算符一起使用 |
| ---------- | ------ | -------------------- |
| +          | 加     | count += 1;          |
| -          | 减     | count -= 1;          |
| *          | 乘     | count *= 1;          |
| /          | 除     | count /= 1;          |
| %          | 模运算 |                      |



## 2.位运算符

| 位运算符 | 语义     |
| -------- | -------- |
| &        | 按位与   |
| \|       | 按位或   |
| ^        | 按位异或 |
| ~        | 一次求反 |
| <<       | 向左移位 |
| >>       | 向右移位 |



## 3.关系运算符

| 关系运算符 | 语义     |
| ---------- | -------- |
| ==         | 等于     |
| !=         | 不等于   |
| <          | 小于     |
| <=         | 小于等于 |
| >          | 大于     |
| >=         | 大于等于 |



## 4.复合条件运算符

| 复合运算符 | 语义 |
| ---------- | ---- |
| &&         | 且   |
| \|\|       | 或   |



# 四、逻辑结构

## 1.选择结构

* `if`

  ```objective-c
  //if结构
  if (expression)
  {
    //program statements
  }
    
  //if else结构
  if (expression)
  {
    //program statements1
  }
  else
  {
    //program statements2
  }
    
  //if else if else结构
  if (expression1)
  {
    //program statements1
  }
  else if (expression2)
  {
    //program statements2
  }
  else
  {
    //program statements3
  }
  ```

  

* `switch`

  ```objective-c
  switch (expression)
  {
    case value1: 
      //program statements1
      break;
    case value2:
      //program statements2
      break;
    case value3:
      //program statements3
      break;
    default:
      //program statements
      break;
  }
  ```

  

* `conditional`

  ```objective-c
  condition ? expression1 : expression2
  ```

  

## 2.循环结构

* `for`循环

  ```objective-c
  for ( init-expression; loop_condition; loop_expression)
  {
    //program statements
  }
  ```

  

* `while`循环

  ```objective-c
  do
  {
    //program statements
  } while (expression);
  ```

  

* `break语句`

  用于退出内层循环

  ```objective-c
  for (int i = 0; i < 10; ++i)
  {
    //program statements
    if (expression)
    {
      break;//满足条件后退出for循环
    }
  }
  ```

  

* `continue语句`

  跳过当前循环

  ```objective-c
  for (int i = 0; i < 10; ++i)
  {
    if (expression)
    {
      continue;//满足条件则跳过当前循环，进入下一循环
    }
    //program statements
  }
  ```

  

# 五、类

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



## 3.数据封装-类的成员变量

类成员变量对外部是隐藏的不能被直接访问。可使用`@property`和`@synthesize`来合成存取方法，供外部调用。例如：

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

从Objective-C 2.0开始，可以使用`@property`自动生成设值方法和取值方法（统称为存取方法）。Xcode4.5开始，`@synthesize`也不需要了，一个`@property`搞定。

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
  //使用点运算符访问属性
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

## 6.覆写`init`方法

```objective-c
- (id) init
{
  self = [super init];
  if(self)
  {
    //初始化代码
  }
  return self;
}
```

注意： `init`被定义为返回`id`类型，这是编写可能被继承的类的`init`方法。例如：

```objective-c
- (id) initWith: (int) n over: (int) d
{
  self = [super init];
  if(self)
  {
    [self setTo: n over:d];
  }
  return self;
}
```

## 7.成员变量作用域指令

实例变量作用域指令包括：

* `@protected`

  这个指令后面的实例变量可被该类及任何子类中定义的方法直接访问。接口部分定义的实例变量默认是这种。

* `@private`

  这个指令后面的实例变量可被定义在该类的方法直接访问，但不能被子类中定义的方法直接访问，在实现部分定义的实例变量默认是这种。

* `@public`

  这个指令后面的实例变量可被该类中定义的方法直接访问，也可被其他类或模块中定义的方法直接访问。

* `@package`

  对于64位映像，可以在实现该类的映像中的任何地方访问这个实例变量。

  

```objective-c
@interface Printer
{
  @private
    int pageCount;
  	int tonerLevel;
  @protected
    //definitions
	
}
//methods definition
@end
```



## 8.成员属性的特性-`@property`的参数

```objective-c
// 或者可以省略strong, 编译器默认取用strong
@property (strong, nonatomic) NSString *nameNonCopy;
```

* 原子性

  比较简单的一句话理解就是：是否给setter和getter加锁(是否保证setter或者getter的每次访问是完整性的)。

  | 参数            | 说明                                                         |
  | --------------- | ------------------------------------------------------------ |
  | atomic （默认） | atomic的作用只是给getter和setter加了个锁。也就是说，有线程在访问setter，其他线程只能等待完成后才能访问。 |
  | nonatomic       | 而用nonatomic，则不保证你获得的是有效值，如果像上面所述，读、写两个线程同时访问变量，有可能会给出一个无意义的垃圾值。 |

* 存取性

  存取特性有**readwrite**(默认值)和**readonly**。

  | 参数              | 说明                           |
  | ----------------- | ------------------------------ |
  | readwrite（默认） | 读写，同时生成getter和setter。 |
  | readonly          | 只读，只生成getter。           |

  

* 内存管理特性

  | 参数           | 说明                                                         |
  | -------------- | ------------------------------------------------------------ |
  | strong（默认） | 表明你需要引用(持有)这个对象(reference to the object)，负责保持这个对象的生命周期。注意，基本数据类型(非对象类型,如int, float, BOOL)，默认值并不是strong，strong只能用于对象类型。 |
  | weak           | 给你一个引用(reference/pointer)，指向对象。但是不会主张所有权(claim ownership)。也不会增加retain count。如果对象A被销毁，所有指向对象A的弱引用(weak reference)(用weak修饰的属性)，都会自动设置为nil。在delegate patterns中常用weak解决strong reference cycles(以前叫retain cycles)问题。 |
  | assign         | 它的作用和**weak**类似，唯一区别是：如果对象A被销毁，所有指向这个对象A的**assign**属性并不会自动设置为nil。这时候这些属性就变成野指针，再访问这些属性，程序就会crash。因此，在ARC下，**assign**就变成用于修饰基本数据类型(Primitive Type)，也就是非对象/非指针数据类型。 |
  | copy           | 会在赋值前，复制一个对象。                                   |
  | retain         | **retain**是以前非ARC时代的特性，在ARC下并不常用。它是**strong**的同义词，两者功能一致。 |

# 六、关键字

## 1.`static`关键字

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

# 

## 2.`self`关键字

`self`关键字是用来指明对象是当前方法的接收者，用于实例的自我调用。例如,在`Fraction`的`add`方法中调用其`reduce`方法：

```objective-c
-(void) add: (Fraction *)f
{
  numerator = numerator * f.denominator + denominator * f.numerator;
  denominator = denominator * f.denominator;
  
  [self reduce];
}
```

## 3.`extern`关键字与全局变量

如果在程序的开始处，所有方法、类定义和函数定义之外定义变量，那么这个变量称为全局变量。

```objective-c
int gMoveNumber = 0;//全局变量gMoveNumber

@interface
{
  //properties definition
}
//methods definition
@end
```

在需要访问外部变量的模块中，需要在声明前加上关键字`extern`,例如：

```objective-c
extern int gMoveNumber;
```



# 七、类的继承

父类的非私有实例变量和方法都会成为新类定义的一部分。子类可以直接访问这些方法和实例变量。需要注意的是，要在子类中直接使用实例变量，必须先在接口部分声明，而不是在实现部分声明。在实现部分声明和合成(synthesize)的实例变量是私有的，子类中并不能直接访问，需要明确定义或合成取值方法，才能访问实例变量的值。

在Objective-C中实例方法的执行规则是这样的：

先检查该对象所属的类，如果没有再检查它的父类。

## 1.继承的作用

* 通过类继承可以扩展添加新的方法
* 通过方法覆写创建特殊版本
* 通过覆写一个或多个方法来改变类的行为

## 2.方法覆写

新建一个同名的方法来替代继承的方法，子类方法必须具有相同的返回类型，并且参数的数目与覆写方法相同。

```objective-c
//父类ClassA类声明
#import <Foundation/Foundation.h>
@interface ClassA: NSObject
{
  int x;
}
-(void) initVar;
@end

//ClassA类实现  
@implementation ClassA
-(void) initVar
{
	x = 100;  
}
@end
```

```objective-c
//子类ClassB类声明
@interface ClassB: ClassA
-(void) initVar;
-(void) printVar;
@end
  
//ClassB类实现
@implementation ClassB
//覆写initVar方法
-(void) initVar
{
  x = 200;
}
//添加新方法
-(void) printVar
{
  NSLog(@"x = %i", x);
}
@end
```



## 3.抽象类

有时创建类只是为了更容易创建子类。在该类中定义方法和实例变量，但不期望任何人从该类创建实例。在Objective-C的语法构造中没有像C++/Java那样专门的abstract class定义。

```objective-c
//  创建类Person 声明如下方法
@interface Person : NSObject
- (void)love;

- (void)coding;

- (void)travelling;

- (void)home;
@end
```

```objective-c
//  在.m文件中最好做如下处理
#define MethodNotImplemented() \
    @throw \
    [NSException exceptionWithName:NSInternalInconsistencyException \
                            reason:[NSString stringWithFormat:@"You must override %@ in a subclass", NSStringFromSelector(_cmd)] \
                          userInfo:nil]

@implementation Person

- (instancetype)init {
    self = [super init];
    if (!self) return nil;
    return self;
}

- (void)work { MethodNotImplemented(); }

- (void)coding {MethodNotImplemented(); }

- (void)love { MethodNotImplemented(); }

- (void)travelling { MethodNotImplemented(); }

- (void)home { MethodNotImplemented(); }

@end
```

```objective-c
#import "Person.h"

@protocol PersonDelegate;

@interface Person ()

@property (nonatomic, copy) NSString *name;

@property (nonatomic, assign) int age;

@property (nonatomic, weak) id<PersonDelegate> delegate;

- (void)eat;

@end

@interface Person(Abstruct)

- (void)work;

@end

@protocol PersonDelegate <NSObject>

- (void)run;

@end
```



# 八、分类

分类提供了一种简单的方式，用它可以将类的定义模块化到相关方法的组或分类中，它还提供了扩展现有类定义的简便方式，并且不必访问类的源代码，也无须创建子类。

## 1.分类的定义与实现

```objective-c
//定义MathOps分类
#import "Fraction.h"
@interface Fraction (MathOps)
  -(Fraction *) add: (Fraction *) f;
	-(Fraction *) mul: (Fraction *) f;
	-(Fraction *) sub: (Fraction *) f;
	-(Fraction *) div: (Fraction *) f;
@end
  
//MathOps分类的实现
@implementation Fraction (MathOps)
  -(Fraction *) add: (Fraction *) f
	{
  	//将两个分数相加
  	Fraction *result = [[Fraction alloc] init];
  	result.numerator = (numerator * f.denominator) + (denominator * f.numerator);
  	result.denominator = denominator * f.denominator;
  	[result reduce];
  	return result;
	}
  -(Fraction *) sub: (Fraction *) f
  {
    //将两个分数相减
    Fraction *result =[[Fraction alloc] init];
    //statements
    return result;
  }
	-(Fraction *) mul: (Fraction *) f
  {
    //将两个分数相乘
    Fraction *result = [[Fraction alloc] init];
    //statements
    return result;
  }
	-(Fraction *) div: (Fraction *) f
  {
    //将两个分数相除
    Fraction *result = [[Fraction alloc] init];
    //statements
    return result;
  }
@end
```

```objective-c
//使用
@autoreleasepool {
  Fraction *a = [Fraction new];
  Fraction *b = [Fraction new];
  Fraction *result = [a sub: b];
}
  
```



## 2.类的扩展（匿名分类）

创建一个未命名的分类，在括号`()`之间不指定名字，这种特殊的语法定义为类的扩展。

```objective-c
@interface Fraction ()
  //properties definition
  //methods definition
@end
```



通常会在类的实现文件中添加类的扩展。



# 九、协议@protocol

协议是多个类共享的一个方法列表，协议中列出的方法没有相应的实现。

## 1.协议的定义

如果类定义决定实现特定的协议，也就意味着要遵守（confirm to）或（adopt）这项协议。协议中有些方法是必须实现的，有些是可以选择实现的。`@optional`指令后面列出的所有方法都是可选的。

```objective-c
@protocol Drawing
  -(void) paint;
	-(void) erase;
	@optional
  -(void) outline; //可选实现

@end
```

```objective-c
//类定义声明实现协议
@interface AddressBook: NSObject<Drawing>
  //properties
  //methods
@end
  
//类定义声明实现多个协议使用","隔开
@interface AddressBook: NSObject<NSCopying,NSCoding>
  //properties
  //methods
@end
  
//分类声明实现协议
@interface Fraction (Stuff) <NSCopying, NSCoding>
  //properties
  //methods
  
@end
```



## 2.协议检查

* 检查对象是否遵循指定协议`confirmToProtocal`

  ```objective-c
  if([currentObject confirmToProtocal: @protocol (Drawing)] == YES)
  {
    //statements
  }
  ```

  

* 检查对象是否实现了协议的可选方法`respondsToSelector`

  ```objective-c
  if([currentObject respondsToSelector: @protocol (outline)] == YES)
  {
    //statements
    [currentObject outline];
  }

## 3.代理概念

协议也是一种两个类之间的接口定义，定义了协议的类可以看做是将协议定义的方法代理给了实现它们的类。这样，类的定义可以更为通用，因为具体的动作由代理类来承担，来响应某些事件或者某些参数。Cocoa和iOS非常依赖代理这个概念。



# 十、动态类型

## 1.`id`类型

这是一种通用的对象类型，也就是说，`id`类型变量可用来存储任何类的实例对象。

```objective-c
id dataValue = [Fraction new];
```

`id`变量声明遵循某个特定协议：

```objective-c
id<Drawing> currentObject;
```



## 2.类对象`class-object`

`class-object`是一个类对象（通常是由`class`方法产生的）。

要根据类名或另一个对象生成一个类对象，可以向它发送`class`消息，如：

```objective-c
//根据类名生成类对象
[Square class];

//根据对象生成类对象
[mySquare class];

//判断两个对象是不是相同的类实例
if ([obj1 class] == [obj2 class])
{
	//statements  
}
```

## 3.`SEL`类型

`selector`是一个`SEL`类型的值（通常是由`@selector`指令产生的）

使用`@selector`指令对指定方法生成一个`SEL`类型：

```objective-c
//NSObject的alloc方法
@selector (alloc)
//多参数方法（例如setTo方法）
@selector (setTo:over:)
```



## 4.`NSObject`提供的处理动态类型的方法

* -(BOOL)  isKindOfClass: class-object

  判断对象是不是`class-object`或其子类的成员

* -(BOOL) isMemberOfClass: class-object

  判断对象是不是`class-object`的成员

* -(BOOL) respondsToSelector: Selector

  判断对象是否能够响应`selector`所指定的方法

* +(BOOL) instancesRespondToSelector: Selector

  判断指定的类实例是否能响应`selector`

* +(BOOL) isSubclassOfClass: class-object

  判断对象是不是指定类的子类

* -(id) performSelector: selector

  应用`selector`指定的方法

* -(id) performSelector: selector withObject: object

  应用`selector`指定的方法，传递参数`object`

* -(id) performSelector: selector withObject: object1 withObject: object2

  应用`selector`指定的方法，传递参数`object1`和`object2`



## 5.多态：相同的名称，不同的类

多态能够使来自不同类的对象定义相同名称的方法。动态类型能使程序直到执行时才确定对象所属的类。动态绑定则能使程序直到执行时才确定实际要调用的对象方法。



# 十一、异常处理

## 1.`try-catch-finally`结构：

```objective-c
@try {
  //statements
}
@catch (NSException *exception) {
  //statements
}
@finally {
  //statements
}
```



## 2.抛出异常`@throw`

`@throw`指令抛出封装后的异常。

抛出异常通常会使用大量的系统资源，所以Apple反对非必要的使用异常。



# 十二、预处理程序

## 1.`#define`语句（宏定义）

`#define`语句的基本用途之一就是给符号名称指定程序常量，经常放在程序的开始，但`#import`或`#include`语句之后。

```objective-c
//指定TRUE为1，FALSE为0
#define TRUE 1
#define FALSE 0
```

符号名称的定义不仅可以包括简单的常量值，也可以包括表达式和其他任何内容。

```objective-c
#define TWO_PI 2.0*3.141592654
#define AND &&
#define OR ||
#define EQUALS ==
//带参数的表达式
#define IS_LEAP_YEAR(y) y % 4 && y % 100 != 0 || y % 400 == 0
#define SQUARE(x) ((x) * (x))
#define MakeFract(x,y) ([[Fraction alloc] initWith: x over: y])
#define MAX(a,b) (((a) > (b)) ? (a) : (b))
#define IS_LOWER_CASE(x) (((x) >= 'a') && ((x) <= 'z'))
//复合表达式
#define TO_UPPER(x) (IS_LOWER_CASE(x) ? (x) - 'a' + 'A' : (x))
```

使用示例：

```objective-c
char c = 'a';
if (IS_LOWER_CASE(c))
{
  //statements
}
```



## 2.`#import`语句

`#import`语句让预处理程序在系统中寻找指定的文件，并且有效地把文件的内容复制到程序中出现`#import`语句的确切位置。

```objective-c
#import "metric.h"
#import <Foundation/Foundation.h>
```

头文件名两侧的双引号指示预处理程序在一个或多个文件目录（通常，首先在包含源文件的目录中查找，但通过修改适当的“项目设置”，可以用XCode指定预处理程序搜索确切位置）中寻找指定的文件。

把文件名放在`<`和`>`之间，将导致预处理程序只在特殊的“系统”头文件目录中寻找文件，当前目录不会被搜索。

## 3.条件编译

* `#ifdef`、`#endif`、`#else`和`#ifndef`语句

  程序有时必须依靠系统相关的参数，这些参数需要在不同的设备或特定版本的操作系统上分别指定。例如：

  ```objective-c
  #ifdef IPAD
  #define KImageFile @"barnHD.png"
  #else
  #define KImageFiel @"barn.png"
  #endif
  ```

  `#ifndef`和`#ifdef`语义相反，判断指定符号是否没有定义，如果指定符号没有定义则执行后续指令否则跳到`#else`指令。

* `#if`和`#elif`语句

  `#if`语句可以用来检测常量表达式是否为非零。如果表达式的结果为非零，就会处理到`#else`、`#elif`或`#endif`为止的所有后续行，否则将跳过它们。

  ```objective-c
  #if defined (DEBUG)
  //处理指令
  #endif
  //等同于
  #ifdef DEBUG
  //处理指令
  #endif
  ```

  

* `#undef`语句

  将一些已经定义的名称符号变成未定义的。

  ```objective-c
  //格式
  #undef 符号名称
  //例子
  #undef IPAD
  ```

  

# 十三、内存管理和自动引用计数

当应用终止时，内存中的所有对象都会被释放，不论它们是否在自动释放池中。

## 1.自动垃圾收集

```objective-c
Build Settings > Objective-C Garbage Collection  设置为Required启用自动垃圾回收
//目前xcode已经没有这个配置项
```

垃圾收集发生在程序运行时，当系统检测到内存到达低位时，就开始清理了。这是一个计算密集的过程，系统追踪所有的对象和引用，检测对象是否正在使用（被引用），这就可能会引起应用的中断。这就是不推荐使用内存收集特性的原因。



## 2.手工引用计数`retain`和`release`

当创建对象时，初始的引用计数为1。为保证对象的存在，每当创建引用到对象需要为引用数加1，手动给对象发送`retain`消息：

```objective-c
[myFraction retain];
```

当不再需要对象时，通过给对象发送`release`消息为引用计数减1:

```objective-c
[myFraction release];
```

当对象的引用计数为0时，系统就知道这个对象不再需要使用了（依照理论，在应用中不再有引用到这个对象）所以给对象发送`dealloc`消息释放它的内存。

注意：当对象被销毁后（它的引用计数减至0，并且调用过`dealloc`方法），对象的引用变得失效。如果你有一个这样的引用，通常被称为悬挂指针（dangling pointer)的引用。给悬挂指针发送消息往往会出现意外，甚至应用发生崩溃。



在大多数情况下，会使用继承自`NSObject`的`dealloc`方法。然而，为了能够释放由对象创建或保持的实例变量或者其他对象，需要覆写`dealloc`方法。例如，在一个类中，有一个`NSArray`类型的实例变量，当类对象销毁的时候，需要释放数组，那么就需要重写`dealloc`方法来做这个事情。



## 3.自动释放池

`````objective-c
//创建一个自动释放池
NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init]
`````

自动释放池可以帮助追踪需要延迟一些时间释放的对象，通过给自动释放池发送`drain`消息，自动释放池会被清理，对象会被释放。

```objective-c
[pool drain];
```

给对象发送`autorelease`消息，将一个对象添加到自动释放池维护的对象列表中：

```objective-c
[result autorelease];
```

```objective-c
- (Fraction *) add: (Fraction *)f
{
  Fraction *result = [[Fraction alloc] init];
  result.numerator = numerator * f.denominator + denominator * f.numerator;
  result.denominator = denominator * f.denominator;
  
  [result reduce];
  return [result autorelease];
  //或者在创建对象时就添加进自动释放池，Fraction *result = [[[Fraction alloc] init] autorelease]
}
```





## 4.事件循环和内存分配

Cocoa和iOS应用运行在所谓的事件循环中。事件是伴随着某些行为或隐性行为而发生的。为了处理这样一个新事件，系统会创建一个新的自动释放池，可能会调用到你应用中的一些方法来处理这个事件，当处理完这个事件，并从你的方法返回后，系统开始等待下一个事件的发生。然而在此之前，系统会清理自动释放池，这就意味着在事件处理过程中创建的自动释放对象都将被销毁，除非对象使用`retain`才能从清空自动释放池的过程中幸存下来。当使用手工引用计数时，你需要对自动释放池进行思考，在事件循环结束后清理自动释放池幸存的这些对象。



## 5.自动引用计数(ARC)

```objective-c
//启用ARC的设置
Build Settings > Objective-C Autorelease Reference Counting
```

自动引用计数（ARC）可以避免手工引用计数的一些潜在陷阱。系统会检测出何时需要保持对象，何时需要自动释放对象，何时需要释放对象，这些你都不用担心。



## 6.强变量

通常所有对象的指针变量都是强变量。也就是说，将对象的引用赋给变量使对象自动保持，然后，旧对象的引用会在赋值前被释放。无论它是实例变量、局部变量还是全局变量。前提是使用自动引用计数（ARC）。

声明强变量关键字：`__strong`

```objective-c
__strong Fraction *f1;
```

```objective-c
@property (strong,nonatomic) NSMutableArray *birdNames;
```

因为对象变量默认都是强变量，所以并不需要声明。

## 7.弱变量

当一个变量被声明为弱变量时，系统会追踪赋值给这个变量的引用。当引用的对象释放时，弱变量会被自动设置为`nil` 。这也避免了无意间给这个变量发送消息引起崩溃的发生。

声明弱变量关键字：`__weak`

```objective-c
__weak UIView *parentView;
```

```objective-c
@property (weak, nonatomic) UIView *parentView;
```



## 8.`@autoreleasepool`块

```objective-c
@autoreleasepool
{
  
}
```

任何在这个上下文中创建的对象都是自动释放的（这是由ARC自动做的），在自动释放池块结束的时候销毁这些对象（除非编译器在自动释放块结束后还需要保证这个对象的存在）。

# 十四、C语言特性

## 1.数组

* 数组定义

  ```objective-c 
  Fraction *fracts [100];//定义
  ```

  ```objective-c
  int integers[5] = {0,1,2,3,4};//初始化
  ```

  

* 字符数组

  ```objective-c
  //没有设定数组长度，自动根据初始化元素的数目确定数组大小
  char word[] = {'H','e','l','l','o','!','\0'};
  NSLog (@"%s", word)
  ```

  

* 多维数组

  ```objective-c
  int M[4][5] = {
    {10,5,-3,17,82},
    {9,0,0,8,-7},
    {32,20,1,0,14},
    {0,0,8,7,6}
  };
  ```

  

## 2.函数

```objective-c
返回值类型 函数名称(参数类型 参数名称,...)
{
  //program statement
  return 返回值；
}
```

如果函数或者方法更改了数组元素的值，那么这个变化将影响到传递到该函数或方法的原始数组，而且这个变化在函数或方法执行完之后依然有效。因为使用数组时，并非将整个数组的内容复制到形参数数组中，而是传递一个指针。

## 3.块（Blocks）

与函数不同的是，块定义在函数或者方法内部，并且能够访问在函数或者方法范围内块之外的任何变量。块是对C语言的一种扩展有。块能够作为参数传递给函数或方法。

块语法格式：

```objective-c
返回类型 (^引用名称) (参数类型,...) = ^(参数类型 参数名,...){
  //块处理程序代码
};//块定义以";"分号结束
```

例如：

```objective-c
//无参数无返回值块
void (^printMessage)(void) = ^(void) {
  NSLog(@"Programming is fun.");
};

printMessage();//执行块
```



一般情况不能在块外部修改已经定义过的变量，除非在定义变量时使用块修改器`__block`。如：

```objective-c
__block int foo = 10;
void (^printFoo)(void) = ^(void){
  NSLog(@"foo=%i", foo);
  foo = 20;
};
foo = 15;
printFoo();//输出15
NSLog(@"foo=%i", foo);//输出20
```

```objective-c
//带返回值和参数的块
int (^gcd) (int, int) = ^(int u, int v) {
  int temp;
  while (v != 0)
  {
    temp = u % v;
    u = v;
    v = temp;
  }
  return u;
};
```



## 4.结构

通过`struct`关键字来定义结构，例如：

```objective-c
//定义结构
struct date {
  int day;
  int month;
  int year;
};
//结构变量的定义和赋值
struct date today;
today.day = 21;
today.month = 6;
today.year = 2012;

//初始化赋值
struct date today = {21,6,2012};
//或者
struct date today = {.day = 21, .month = 6, .year = 2012};
//也可以部分赋值
struct date today = {.year = 2012};
```

结构中的结构：

```objective-c
typedef struct CGPoint CGPoint;
typedef struct CGSize CGSize;
struct CGRect {
  CGPoint origin;
  CGSize size;
};
```

简化与灵活的运用方式：

```objective-c
struct date {
  int day;
  int month;
  int year;
} today = {21, 6, 2012};

//或者
struct {
  int day;
  int month;
  int year;
} today = {21, 6, 2012};
//结构数组
struct {
  int day;
  int month;
  int year;
} dates [100];
```



## 5.指针





