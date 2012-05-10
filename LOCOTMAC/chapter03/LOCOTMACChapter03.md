###Chapter 3 - Introduction to Object-Oriented Programming

    As we dive into OOP, stick a Babel fish in your ear, and be prepared to encounter
    some strang terminology along the way.

**stick a Babel fish in your ear** 这个短语不知道该怎么翻译会比较好。

#### It's All Indirection
看了这么多关于面向对象的书籍，对于 Indirection 的描述倒还是第一次看到。下面的这段描述到蛮有意思的。

    An old saying in programming goes something like this, "There is no problem in 
    computer science that can't be solved by adding another level of indirection."

    Indirection is a fancy word with a simple meaning - instead fo using a value 
    directly in your code, use a pointer to the value. Here's a real-word example:
    you might not know the phone number of your favorite pizza place, but you know
    you can look in the phone book to find it. Using the phone book is like a form 
    of indirection.

计算机永不知疲倦，可以永远 Indirection 下去。

    This runaround is a form of indirection. Luckily, computers have infinite 
    patience and can handle being sent from place to place to place looking for
    an answer.

##### Indirection Throuth Filenames

    We're leaving out the time stamp and process ID that NSLog() adds to the output 
    of Word-Length-1.

在 C 程序中，会将 **\n** 当成一个字符计数，为了防止这种情况的发生通常都会用 **\0** 进行替换操作。

在通常的测试中，会将程序中用到的临时文件存放在 /tmp 文件夹中，对于需要长期持有的文件可不能这样做哟。看看对于 /tmp 文件夹有趣的说明。

    Take a look at the path name we used with fopen(). It's /tmp/words.txt. This mean
    that the words.txt is a file that lives in the /tmp directory, the Unix temporary
    directory, which get emptied when the computer reboots. You can use /tmp to store
    scratch files that you want to mess around with but really don't about keeping. 
    For a real, live program, you'd put your file in a more permanent location, such
    as the home directory.

######Word-Length-3 project
作者提供的预编译版本会自动帮助拷贝文件，可以查看一下是如何实现的。

######Word-Length-4 project

    Tell program to "go look at first launch parameter of the program to figure 
    out the location of the words file."

使用过 Visual Studio/Eclipse 开发环境的人都知道，可以在集成开发环境中直接为程序提供参数。下面是 xcode 中的做法。

    Because you're supplying arguments at runtime, everybody can use your program
    to get the length of any set of the words they want to, even absurdly large 
    sets of words. Users can change the data without changing the code, just as
    the nature intended. This is the essence of tht indirection:
    it's telling us where to get the data we need.

#### Using Indirection in Object-Oriented Programming

##### Procedural Programming

###### A HANDY SHORTCUT

    The rectangles in the Shapes-Procedural program's main() method are declared using a handy little C trick:
    when you declare a variable that's a structure, you can initialize all the elements of that structure at 
    once.
        ShapeRect rect0 = { 0, 0, 10, 30 };
    The structure elements get value in the order they're declared. Recall that ShapeRect is declared like this:
        typedef struct {
            int x, y, width, height;
        } ShapeRect;
    
##### Implementing Object Orientation

    Procedural programs are based on functions. The data orbits around the functions. Object orientation revert
    this point of view, placing a program's data at the center, with the function orbits the data. Instead of 
    focusing on functions in your programs, you concentrate on the data.
    
Objective-C 很好的使用了消息机制，如果希望某对象采取某种动作，只需要 **sending a message** (although some folks also say "calling a method") 即可，
具体的操作交由实现完成。

Objective-C 对象有一个指向其 class 的指针，class 告诉了这个对象是什么，能做什么。

###### 这里提到了这样一个问题

    What's the point of having class object? Wouldn't it be simpler just have each object point directly to its code?
    Indeed, it would be simpler, and some OOP systems do just that. 
    But having class object is a great advantage: if you change class at runtime, all objects of that class automatically
    pick up the changes 
    
JavaScript 采用对象继承的方式创建对象，也就是这所说的，直接指向对应的代码，在某些应用下确实还是比较方便的。

#### Time Out for Terminology

  * class - Objective-C style encourges developers to capitalize class names.
  * object - An object is a structure containing values and a hidden pointer to its class. Objective-C variables that refer
           - to objects are typically not capitlized.
  * instance - is another word for "
  * message - is an action that an object can perform.
            - This is what you send to an object to tell it to do something.
            - In the [shape draw] code, the draw message is sent to the shape object to tell it to draw itself.
            - When an object receives a message, its class is consulted to find the proper code to run.
  * method - A method is code that runs in response to a message.
  * method dispatcher - is a mechanism used by Objective-C to divine which method to be executed in response to a particular message.
  * interface - is the description of the features provided by a class of objects.

对于接口 interface 这个概念，不要仅局限于 OOP 中。

    The concept of interfaces is not limited to OOP. For example, header files in C provide interfaces
    for libraries such as the standard I/O library (which you get when you #include <stdio.h>), and the
    math library (#include <math.h>). Interfaces do not provide implementation details, and the general
    idea is that you shouldn't care about them.

  * implementation - is the code that makes interface work.

----

#### OOP in Objective-C

##### The @interface Section
在大一点的项目中，我们会将每个类放置在各自的文件中。

在 Objective-C 中牢记，只要以 **@** 开头的内容，都属于对 C 语言的扩展。


##### GET YOUR INFIX HERE (p46)
Objective-C 使用 **中缀法 infix notation** 进行语法标记，方法、参数的名称编结在一起显示。这么做的原因是，通常 C 语言中一个
方法可能会有多个参数，在没有参看文档的情况下很难了解各项的含义，而中缀法需要你将参数以 **名值对** 的形式传递给方法，这样
做可以让你更方便的 编程。

##### CALLIN' ALL COLONS (p47)

    The rule to follow is this:
    If a method takes an argument, it has a colon.
    If it takes no arguments, it has no colons.

##### The @implementation Section
学到了一个新词 **TLA** 。

    The interface is often called the API, which is a TLA for "application programming interface" (
    and TLA is a TLA for "three-letter acronym"). The actual code to make object work is found in the 
    @implementation section.

学习 JavaScript 时提到过这样一个问题，JavaScript 没有相应的作用域控制，而这里的 Objective-C 实际上也没有 public、
private 一说。

    You might think that define a method solely in the @implementation directive make it inaccessible from 
    the outside the implementation, but that's not the case. Objective-C doesn't really have private methods.
    There is no way to mark a method as being private and preventing other code from calling it.
    This is side effect of Objective-C's dynamic nature.

###### cut and past programming

    One drawback to cut and past programming, like our Triangle class, is that it tends to careate a lot of 
    duiplicated code, like the setBounds: and setFillColor: methods. We'll introduce you inheritance in the 
    next chapter, which is a fine way to avoid redundant code like this.
    
###### Open/Closed Principle
这里讲到了设计模式里的 **开闭原则** 。


#### Summary


  
    






















s