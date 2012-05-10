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
    