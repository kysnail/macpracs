###Chapter 2 - Extensions to C

#### Building Hello Objective-C
本章提到，如果你没有使用过 xcode ，可以参考 **Learn C on the Mac** 这本书的第二章，有很详细的介绍。

本书源码下载地址 Learn ObjC Projects

Xcode 通常位于 **/Developer/Applications** 这个目录下。

#####Mac 下的命令行项目位于

    Command Line Utility -> Foundation Tool

对于 xcode 4.2 来说，操作流程稍有不同。首先在 Application 项目中选择 Command Line Tool ，然后在接下来的项目属性设置界面中，选择 Foundation 类型即可。

Objective-C 源码文件的扩展名为 *.m 。

通常系统为你生成的 boilerplate 比较复杂，这里最简单的程序可以写成下面的样式：

    #import <Foundation/Foundation.c>
    
    int main (int argc, const char *argv[])
    {
        NSLog (@"Hello, Objective-C!");

        return (0);
    } // main

编译这个简单的 Objective-C 程序可能会用到的快捷键

    编译并运行 - Build and Go - ❀R
    打开 xcode 控制台窗口 - Open the Xcode console window - ❀↑R

在 xcode 开发环境中，*.m 文件被 Objective-C 编译器处理，*.c 文件被 C 编译器处理，而 *.cpp 被 CPP 编译器编译，但这三种语言其实最终都是被 gcc 处理。

为什么扩展名是 *.m 呢？

    The .m extension originally stood for "messages" when Objective-C was first 
    introduced, referring to a central feature of Objective-C that we'll talk 
    about in the future chapters. Nowadays, we just call them dot-m files.

C 语言中使用 include 导入头文件，在 Objective-C 中也可以这样做。但在实际中你可能永远都不会。

使用过 C 语言的人都知道，include 这种引入方式，很难避免重复、递归应用。为了避免这种情况的出现，通常通过大量的使用 #ifdef 等控制死循环。而在 Objective-C 中，#import 可以很好的解决这个问题。

而实际上，**#import** 语句是由 gcc 提供的，xcode 将其引用到开发环境中。这个特性我倒是第一次看到，也不知道其他的集成开发环境是否有提供 **#import** 的支持。

#### What is framework?
这是一个好问题，框架这个词只要从事软件开发的可能没有没听过的吧。但具体什么是框架，则各有个的解释了。

比如 jQuery 只能算得上是库，并不是框架。

框架是一系列部件的集合——头文件、库、图片、声音等等。Apple 将 Cocoa、Carbon、QuickTime、OpenGL 等框架组合成一个更大的框架集。

Cocoa 由两个子框架集

    * Foundation
    * Application Kit (also known as AppKit)

以及一组支援框架组成，包括 Core Animation 和 Core Image ，这些支援框架为 Cocoa 框架提供了非常绚丽的效果。

**Foundation framework** 处理的事物，通常位于 user interface 以下的层。诸如数据结构、通讯机制等。本书所有的程序都是基于 Foundation framework。

    Note:
    一旦你学完这本书，在你成为 Cocoa guru 的道路上，下一个需要掌握的就是 Cocoa's Application Kit 了。

    Once you finished this book, your next step along the road to becoming a 
    Cocoa guru is to master Cocoa's Application Kit, which contains Cocoa's 
    high-level features: user interface elements, printing, color and sound
    management, AppleScript support, and so on. To find out more, check out 
    Learn Cocoa on the Mac by Dave Mark and Jeff LaMarche (Apress 2009).

这里推荐的第二本书 **Learn Cocoa on the Mac** 。

整个 Foundation framework 占据了大概 1M 的磁盘空间，包含大约 14,000 行代码，分散在大约一百多个文件中。当你引入 **#import <Foundation/Foundation.h>** 头文件时，你就获得了整个集合。你可能会想，一下导入这么多的代码，会让编译工作变得缓慢？还好 xcode 为我们想到了这点，会在这个阶段进行相应的优化工作。

如果你想查看 Foundation.h 的具体内容，可以系统的下述位置进行查找。

    /System/Library/Frameworks/Foundation.framework/Headers/

#### NSLog() and @"strings"

    NSLog (@"Hello, Objective-C!");

使用 NSLog 的同时，实际上就在享用 Cocoa 给我们编写 C 程序带来的好处。此程序对应的 C 语言版本，会使用到 printf() 进行文本的输出工作。

当然在 Objective-C 中也可以使用 printf() 进行 console 的输出，但并不推荐这么做。因为 NSLog() 提供了很多有用的特性，帮助我们实现一些常见的工作。诸如日期/时间戳，自动在行尾补全 '\n' 字符等。

比如在控制台中会看到没一条语句前面都会有相应的时间戳等信息，这实际上就是由 NSLog() 生成的。

**NSLog()** 头一回看起来总有些别扭，怎么起了这样一个名字，说简单了，是为解决名称冲突 **name collisions** 的问题。Cocoa 框架在所有的函数、常量、类型名前缀上 NS 前缀，用来表明属于 Cocoa 框架的内容。

NS 是 NextSTEP 的简写。

这里没有一个集中的前缀注册表，所以你可以选择你所想要的前缀。但有一条原则需要牢记，不要在你的函数或变量前添加 NS 前缀，此前缀默认归 Apple 私有了。

另外一个需要注意的地方，就是双引号前的 @ 符，这个符号也是 Objective-C 增加的一个特性，由 @ 引导的字符串，会被处理为 Cocoa 框架下的 NSString 元素。

NSString 元素相比 C 语言本身自带的字符串处理机制要强大得多。它将很多常见的字符串处理工作封装成 NSString 的方法，处理起来很方便，比如：

  * 查询字符串长度
  * 对比字符串
  * 将数字字符串转换为整型或浮点型

关于 NSString 的内容将在第 8 章讲述。

##### WHAT THOSE STRINGS
一个常见的错误是将 C-style 的字符串传递给 NSLog() 函数，而不是使用 NSString 类型的元素。这种情况下，编译器会报以警告信息，如果运行这样的程序，则可能有崩溃的危险。所以建议在 xcode 中设置如下内容

    Treat Warnings as Errors

以此保证所写代码能够正常编译通过。

##### Cool fact about NSString
Cocoa 还有一个特性即所有的类型命名具有自明示的效果，通过名称就可以判断该元素具有哪些特性。比如下面的内容：

  * NSArray provides arrays
  * NSDateFormatter helps you format dates in different ways
  * NSThread gives you tools for multithread programming
  * NSSpeechSynthesizer lets you hear speech

####Are You the Boolean Type?
Objective-C 所提供的 Boolean 类型比较有趣，


