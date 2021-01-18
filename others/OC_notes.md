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

//类名首字母大写
//属性以下划线开头

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

