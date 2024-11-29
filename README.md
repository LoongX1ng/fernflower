### About FernFlower

FernFlower is the first actually working analytical decompiler for Java and 
probably for a high-level programming language in general. Naturally it is still 
under development, please send your bug reports and improvement suggestions to the
[issue tracker](https://youtrack.jetbrains.com/newIssue?project=IDEA&clearDraft=true&c=Subsystem+Java. Decompiler).

### FernFlower and ForgeFlower

FernFlower includes some patches from [ForgeFlower](https://github.com/MinecraftForge/ForgeFlower).
Sincere appreciation is extended to the maintainers of ForgeFlower for their valuable contributions and enhancements.

### Licence

FernFlower is licenced under the [Apache Licence Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

### Running from command line

`java -jar fernflower.jar [-<option>=<value>]* [<source>]+ <destination>`

\* means 0 or more times\
\+ means 1 or more times

\<source>: file or directory with files to be decompiled. Directories are recursively scanned. Allowed file extensions are class, zip and jar.
          Sources prefixed with -e= mean "library" files that won't be decompiled, but taken into account when analysing relationships between 
          classes or methods. Especially renaming of identifiers (s. option 'ren') can benefit from information about external classes.

包含将要被反编译的文件的文件或目录。允许的文件扩展有class，zip和jar。带有前缀-e=的源意思是“library”文件，这样的文件不会被反编译。但在分析类或方法之间的关系时需要考虑。特别是标识符的重命名（s. option 'ren'）可以从外部类的信息中获益。

\<destination>: destination directory 

目标目录

\<option>, \<value>: a command-line option with the corresponding value (see "Command-line options" below).

一个命令行选项和对应的值（详见下文“Command-line options”）。

##### Examples:

`java -jar fernflower.jar -hes=0 -hdc=0 c:\Temp\binary\ -e=c:\Java\rt.jar c:\Temp\source\`

`java -jar fernflower.jar -dgs=1 c:\Temp\binary\library.jar c:\Temp\binary\Boot.class c:\Temp\source\`

### Command-line options

With the exception of mpm and urc the value of 1 means the option is activated, 0 - deactivated. Default 
value, if any, is given between parentheses.

除mpm和urc外，值为1表示选项被激活，0表示选项被停用。如果有默认值，则在括号之间给出。

Typically, the following options will be changed by user, if any: hes, hdc, dgs, mpm, ren, urc 
The rest of options can be left as they are: they are aimed at professional reverse engineers.

通常情况下，以下选项会被用户更改（如果有这些选项的话）：hes、hdc、dgs、mpm、ren、urc

其余的选项可以保持原样：它们针对的是专业的逆向工程师。



- rbr (1): hide bridge methods

    隐藏桥接方法

- rsy (0): hide synthetic class members

    隐藏合成类成员

- din (1): decompile inner classes

    反编译内部类

- dc4 (1): collapse 1.4 class references

    折叠1.4类引用

- das (1): decompile assertions

    反编译断言

- hes (1): hide empty super invocation

    隐藏空的super调用

- hdc (1): hide empty default constructor

    隐藏空的默认构造函数

- dgs (0): decompile generic signatures

  反编译通用签名

- ner (1): assume return not throwing exceptions

  假定return不抛出异常

- den (1): decompile enumerations

    反编译枚举

- rgn (1): remove getClass() invocation, when it is part of a qualified new statement

    当getClass（）调用是限定new语句的一部分时，删除它

- lit (0): output numeric literals "as-is"

    按原样输出数值字面量

- asc (0): encode non-ASCII characters in string and character literals as Unicode escapes

    将字符串中的非ascii字符和字符字面量编码为Unicode转义

- bto (1): interpret int 1 as boolean true (workaround to a compiler bug)

    将int 1解释为boolean true（编译器的一个bug的解决方法）

- nns (0): allow for not set synthetic attribute (workaround to a compiler bug)

    允许不设置synthetic属性（编译器的一个bug的解决方法）

- uto (1): consider nameless types as java.lang.Object (workaround to a compiler architecture flaw)

    可以把无名类型视作java.lang.Object（编译器架构缺陷的解决方法）。

- udv (1): reconstruct variable names from debug information, if present

    如果有调试信息，则从调试信息中重建变量名

- ump (1): reconstruct parameter names from corresponding attributes, if present

    如果有相应属性，则从相应的属性中重建参数名

- rer (1): remove empty exception ranges

    移除空的异常范围

- fdi (1): de-inline finally structures

    解除finally结构的内联

- mpm (0): maximum allowed processing time per decompiled method, in seconds. 0 means no upper limit

    反编译每个方法允许的最大处理时间，单位为秒。0表示没有上限

- ren (0): rename ambiguous (resp. obfuscated) classes and class elements

    重命名歧义的(例如， 混淆)类和类元素

- urc (-): full name of a user-supplied class implementing IIdentifierRenamer interface. It is used to determine which class identifiers
           should be renamed and provides new identifier names (see "Renaming identifiers")

    用户提供的实现IIdentifierRenamer接口的类的全名。它用于确定应该重命名哪些类标识符，并提供新的标识符名称（请参阅“重命名标识符”）。

- inn (1): check for IntelliJ IDEA-specific @NotNull annotation and remove inserted code if found

    检查IntelliJ特有的@NotNull注解，如果发现有，则删除插入的代码

- lac (0): decompile lambda expressions to anonymous classes

    将lambda表达式反编译为匿名类

- nls (0): define new line character to be used for output. 0 - '\r\n' (Windows), 1 - '\n' (Unix), default is OS-dependent

    定义用于输出的新行符。0 - '\r\n' (Windows)，1 - '\n' (Unix)，默认值取决于操作系统

- ind: indentation string (default is 3 spaces)

    缩进字符串（默认为3个空格）

- crp (0): use record patterns where it is possible

    尽可能使用记录模式

- cps (0): use switch with patterns where it is possible 

    在可能的情况下使用switch的模式

- log (INFO): a logging level, possible values are TRACE, INFO, WARN, ERROR

    日志级别，可能的值是TRACE， INFO， WARN， ERROR

- iec (0): include entire class path into context when decompiling 

    在反编译时，将整个class path包含到上下文中

- isl (1): inline simple lambda expressions

    内联简单lambda表达式

- ucrc (1): hide unnecessary record constructor and getters

    隐藏不必要的记录构造函数和getter函数

- cci (1): check if resource in try-with-resources actually implements `AutoCloseable` interface

    检查try-with-resources中的资源是否实现了‘AutoCloseable’接口

- jvn (0): overwrite any local variable names with JAD style names

    用JAD风格的名称覆盖任何局部变量名称

- jpr (0): include parameter names in JAD naming

    在JAD命名中包含参数名称

### Renaming identifiers

重命名标识符

Some obfuscators give classes and their member elements short, meaningless and above all ambiguous names. Recompiling of such
code leads to a great number of conflicts. Therefore it is advisable to let the decompiler rename elements in its turn, 
ensuring uniqueness of each identifier.

有些混淆器会让类及其成员元素的名称变为简短、无意义，甚至是有歧义的名称。重新编译这样的代码会导致大量的冲突。因此，建议让反编译器依次重命名元素，确保每个标识符的唯一性。

Option 'ren' (i.e. -ren=1) activates renaming functionality. Default renaming strategy goes as follows:

选项‘ren’（即-ren=1）激活重命名功能。默认的重命名策略如下：

- rename an element if its name is a reserved word or is shorter than 3 characters

  如果元素名是保留字或短于3个字符，则重命名元素

- new names are built according to a simple pattern: (class|method|field)_\<consecutive unique number>  
You can overwrite this rules by providing your own implementation of the 4 key methods invoked by the decompiler while renaming. Simply 
pass a class that implements org.jetbrains.java.decompiler.main.extern.IIdentifierRenamer in the option 'urc'
(e.g. -urc=com.example.MyRenamer) to FernFlower. The class must be available on the application classpath.

  新名称是根据一个简单的模式构建的：（类|方法|字段）_\<连续唯一编号>
  您可以通过提供反编译器在重命名时调用的4个关键方法的私人实现来重写此规则。只需将实现org.jetbrains.java.decompiler.main.extern.IIdentifierRenamer的类作为参数（例如-urc=com.example.MyRenamer）传递给FernFlower即可。类必须在应用程序classpath中可用。

The meaning of each method should be clear from naming: toBeRenamed determine whether the element will be renamed, while the other three
provide new names for classes, methods and fields respectively.  

每个方法的含义都应该能从其命名清楚地知悉：toBeRenamed确定元素是否会被重命名，而其他三个分别为类、方法和字段提供新名称。
