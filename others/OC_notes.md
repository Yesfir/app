1. OC完全兼容C语言（算是改进
2. OC源文件后缀名.m，代表message->消息机制
3. import，预编译，imclude增强版，只包含一次

4. 框架：
   1. 事先写好的功能集，封装在类或函数中
   2. Foundation框架：输入输出、数据类型等，其中的.h头文件包含了框架中其他所有头文件

5. @autoreleasepool 自动释放池，代码写在这里，或者整个删掉
6. NSLog
   1. F框架中的函数，printf的增强版，向控制台输出信息
   2. NSLog(@"格式控制字符串", 变量列表);
   3. 增强：输出调试相关信息，执行时间、程序名、pid、tid；自动换行；新增数据类型

```objective-c
#import <Foundation/Foundation.h>
int main(int argv, int ){
  @autoreleasepool{
    NSLog(@"Hello, World!");	//第一个参数前一定要加@
  }
  return 0;
}

float f1=12.12f;	//不加f默认double型占8字节
NSLog(@"jack f1= %f", f1);	//
>>xxxxxx jack f1 = 12.120000
```

7. 字符串

   1. C语言：字符数组，字符指针
   2. OC：NSString 类型的指针变量，用来存储OC字符串的地址
   3. 必须使用前缀@符号

   ```objective-c
   NSString *str=@"jack";
   ```

   4. 如果使用NSLog输出OC字符串，占位符是%@

8. NS前缀，NextStep--->Cocoa--->Foundation框架中



1. 编译（预处理，检查语法，编译）、链接、执行

   ​	cc -c main.m

   ​	cc main.o -framework Foundation

2. OC除了C支持的数据类型，还有：

   1. BOOL: YES, NO，本质是 signed char
   2. Boolean: true, false，本质是unsigned char
   3. class 类
   4. id类型——万能指针
   5. nil 与NULL差不多
   6. SEL 方法选择器
   7. block 代码段



类是模板，对象是根据模板创建的，绝对不多不少。

设计三要素：名字、特征、行为

```objective-c
/*
类是模板，对象是根据模板创建的，绝对不多不少。
设计三要素：名字、特征、行为

类
_____________
｜属性				｜
｜					 ｜
｜__________｜
｜方法				｜
｜					 ｜
｜					 ｜
｜__________｜


类的定义分为两个部分：

->类的声明
@interface 类名：NSObject{
	共同特征定义的变量->属性
}
方法的声明
@end

->类的实现
@implementation 类名
方法的实现
@end

*/

//类名首字母大写!
//属性以下划线开头!

#import <Foundation/Foundation.h>

@interface Person : NSObject{
  NSString *_name;
  int _age;
  float _height;
}
//方法声明：-（类型）名称
- (void)run;
- (void)eatWith:(NSString *)foodName;
- (int)sum:(int)num1 :(int)num2;
//- (int)sumWith:(int)num1 and:(int)num2;
//- (int)sumWithNum1:(int)num1 andNum2:(int)num2;
@end
  
//方法实现
@implementation Person
- (void)run{
}
- (void)eatWith:(NSString *)foodName{
}
- (int)sum:(int)num1 :(int)num2{
}
@end
  
int main(int argc, const char * argv[]){
  //创建类的对象:类名 *对象名=[类名 new]
  Person *p1 = [Person new];
  //默认情况下对象属性不允许被外界访问，否则加@public声明
  @public
  NSString *_name;
  p1->_name=@"jack";
  (*p1)._name=@"jack";
  //调用方法
	[p1 run];
  [p1 eatWith:@"红烧排骨"];
  int sum=[p1 sum:10 :20];
}
```



内存五大区域：

栈：局部变量

堆：malloc, calloc, realloc

BSS段：未被初始化的全局变量、静态变量

数据段（常量区）：已被初始化的全局变量、静态变量、常量

代码段：程序代码



类加载

当某个类第一次被访问到，会将类存储到代码段，程序结束才被释放

Person *p1，在栈中申请Person类型指针变量

[Person new]：在堆中申请空间，根据类模板创建对象、声明属性(0, NULL, nil)，isa指针指向代码段，返回地址给p1指针

对象中只有属性没有方法，属性+isa指针



分组导航标记

```objective-c
#pragma mark 狗狗类的声明
#pragma mark -
#pragma mark - 分组名
```



多文件开发

推荐一个类独占一个模块: NewFile -> Cocoa Class

一个模块至少包含两个文件：.h头文件（类的声明）+.m实现文件（类的实现）

```objective-c
main.m: #import "Person.h"
Person.h: #import <foundation/Foundation.h>
Person.m: #import "Person.h"
```

头文件定义通用结构，例如

```objective-c
// Gender _gender;
typedef enum{
  GenderMale;
  GenderFeMale;
} Gender;
```



类的本质是自定义数据类型，可以作为方法的参数

形参也在栈中开辟了空间，内容同实参

对象也可以作为方法的返回值，返回值类型为类指针



如果一个对象的属性是另一个对象的指针，并不是对象！！（用不了方法，改不了属性

需要新建一个对象，将该指针指向该对象



```objective-c
rewind(stdin);
scanf("%d",&userSelect);
//类的方法中调用当前对象另一方法，self代表当前对象
[self fistTypeWithNumber:userSelect];

#import <stdlib.h>
int x=arc4random_uniform(3)+1;

#import <math.h>
double z=sqrt(x+y);
```



```objective-c
/*异常处理
目的：异常而不崩溃
语法：try catch (finally)
将有可能异常的代码放在@try中，异常时会跳转到@catch
*/
@try{}
@catch(NSException *ex){
  NSLog(@"%@",ex);				//%@打印指针对象，异常原因
}
@finally{
  
}
//避免异常最常用还是逻辑判断
```



```objective-c
// OC中的方法：对象/实例方法<->类方法：
// 声明实现：只有加减号不一样
- (void)sayHi;
+ (void)sayHi;
//调用：[类名 类方法名];
//类方法规范：提供同名类方法，创建返回
@interface Person:NSObject{
  
}
+ (Person *)person;
+ (person *)personWithName:(NSString *)name;
@end
@implementation{
  + (Person *)person{
    Person *p1=[Person new];
    return p1;
  }
}
@end
```



```objective-c
//NSString类
NSString *str0=[NSString new];
NSString *str1=[NSString string];
NSString *str2=[NSString stringWithForm:@"jack"];
NSString *str=@"jack";
//常用类方法
+ (instanceType)stringWithUTF8String:(const char *)nullTerminatedCString;
char *str0="rose";
NSString *str1=[NSStringWithUTF8String:str0];
//instanceType 作为返回值，代表返回的是当前类的对象，将C字符串转换为OC字符串对象，用途：接收scanf等
+ (instanceType)stringWithFormat:(NSString *)foramt;
NSString *name=@"xiaoming";
NSString *s=[NSString stringWithFormat:@"大家好，我叫%@",name];
//常用对象方法
NSString *str=@"Yesfir";
NSUInteger len=[str length];	//%lu
- (unichar)characterAtIndex:(NSUinterger)index; //%c, unichar中文输出%C
unichar ch=[str characterAtIndex:2];
//判断相同不要用==
BOOL com=[str1 isEqualToString:str2];
//比较字符串大小
NSComparisonResult res = [str1 compare:str2];	//可以用int,-1小于
```



匿名对象：没有指针指向这个对象

[[Person new] sayHi];

面向对象三大特征：封装、继承、多态



```objective-c
/*属性的逻辑验证
1. 不能写public，不然外界可以直接访问属性，任意赋值
2. 为类提供方法setter，专门为属性赋值
	a. 这个方法一定是对象方法
	b. 无返回值
	c. 方法名称以set开头跟上属性去下划线首字母大写
	d. 一定有参数，类型与属性参数一致，名称与属性去下划线
	e. 在方法实现中逻辑验证
	f. 外界赋值则调用对象的setter方法
*/
@interface Person:NSObject{
  int _age;
}
- (void)setAge:(int age);
@end
  
@implementation
- (void)setAge:(int)age{
if (age>=0 && age<=200){
  _age=age;}
  else{_age=18;}
}
@end

  
//getter方法，方法名就是属性名
- (int)age{
  return _age;
}

```



组合关系、依赖关系、关联关系、继承关系

组合关系：计算机由CPU等组成

依赖关系：人类的打电话方法需要电话参数，人类依赖于电话类

耦合度：修改一个对象对另一个对象的影响程度

​		低耦合/高耦合；高内聚，单一职责原则

关联关系：人和狗（拥有）



框架、类、函数，怎么用？->Xcode文档

OC中的static关键字

- 不能修饰属性和方法

- 可以修饰方法中的局部变量，变成静态变量存储在常量区，下次执行时直接使用而不会声明
- 应用：类方法创建学生对象时自动编号

self: 指针，在对象方法中指向当前对象，在类方法中指向当前类

取类在代码段中地址的方式：

1. 调试查看对象isa指针的值
2. 类方法中查看self的值
3. 调用对象/类的class方法



多个类具有相同的成员->继承

```objective-c
#import "Person.h"
@interface Chinese : Person
@end
@implementation Chinese
@end
/*
Chinese类从Person类继承，子类，父类/派生，派生类，基类
创建时即可指认
满足集成的关系：is a
如果有成员不是所有子类都拥有，则不该定义在父类
1.单根性 2.传递性
NSObject类，类方法new用来创建对象，isa指针属性
*/
```

super关键字：

1. 类方法和对象方法中
2. 在对象方法中用super调用继承父类的对象方法(相当于self)



访问修饰符：修饰类的**属性**，限定对象属性的访问范围

@private: 私有，本类方法实现中访问

@protected: 受保护的，本类以及本类的子类中访问

@package: 可以在当前框架中访问

@public: 公共，任意地方访问(不要用)

未制定时默认的是protected

子类仍然可以继承父类的私有属性，只不过在子类中无法直接访问

作用域：直到下一个@或者}

想让属性完全真私有(不提示)：把属性定义在implementation的大括号中

私有方法：只写实现不写声明，则不能在外界调用



里氏替换原则：子类替换父类的位置且程序功能不受影响

Person *p2=[Student new];

应用：数组的元素不同类型，例如NSObject *objs[3] 可以存任意OC对象

方法中的参数对象也可以传子类对象

父类指针指向子类对象，通过这个指针只能调用子类对象的父类成员



方法重写：子类有父类的行为但具体实现不同

直接在implementation中实现同样的方法

父类指针指向子类对象，如果方法重写了，则调用子类方法



多态

同一个行为对不同事物有不同的表现形式

例：三个人，不同国籍，同一个sayHI方法，子类重写



NSLog当用%@打印对象：调用方法的description，NSString输出

@"<所属类名：对象地址>"

希望打印自定义字符串：重写description方法



子类对象中有自己的属性和所有父类的属性(isa指向自己代码段)

子类代码段中也有一个isa指向其父类



结构体与类的相同点：多个数据封装为1个整体

struct Date{int year; int month; int day;};

@interface Date:NSObject{int year; int month; int day;}@end

不同点：数据/数据+行为

结构体变量分配在栈空间(相对较小但效率高)，对象分配在堆空间

赋值：变量/指针地址



类第一次被访问时被加入到代码段

一旦被加载直到程序结束不会被回收

在代码段存储类的步骤：

1. 在代码段中创建一个Class对象(Class是Foundation中的1个类)
2. 将类的信息存储在这个Class对象
3. 对象至少有：类名，属性s，方法s，isa(指向存储父类的类对象)



91/209

