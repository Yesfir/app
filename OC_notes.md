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

