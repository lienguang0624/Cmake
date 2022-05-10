# Cmake
## 1. 准备工作
&emsp;&emsp;准备待编译C文件与CMakeList.txt
```c
//main.c 
#include <stdio.h> 
int main() 
{ 
 printf(“Hello World from t1 Main!n”); 
 return 0; 
}
```

```c
PROJECT (HELLO) 
SET(SRC_LIST main.c) 
MESSAGE(STATUS "This is BINARY dir " ${HELLO_BINARY_DIR}) 
MESSAGE(STATUS "This is SOURCE dir "${HELLO_SOURCE_DIR}) 
ADD_EXECUTABLE(hello SRC_LIST)
```

## 2. 开始构建
1. 在`CMakeList.txt`所在目录shell中`cmake .`,将会自动生成`Makefile`文件
2. 然后进行工程的实际构建，在这个目录输入 make 命令
3. 这时候，我们需要的目标文件 hello 已经构建完成，位于当前目录
4. `/hello `得到输出`Hello World from Main`

## 3. 语法解析
**PROJECT 指令的语法是：**\
&emsp;&emsp;`PROJECT(projectname)`\
&emsp;&emsp;你可以用这个指令定义工程名称，并可指定工程支持的语言，支持的语言列表是可以忽略的，默认情况表示支持所有语言。

**SET 指令的语法是：**\
`SET(VAR [VALUE] [CACHE TYPE DOCSTRING [FORCE]]) `\
&emsp;&emsp;现阶段，你只需要了解 SET 指令可以用来显式的定义变量即可\
&emsp;&emsp;比如我们用到的是 `SET(SRC_LIST main.c)`，如果有多个源文件，也可以定义成：\
&emsp;&emsp;`SET(SRC_LIST main.c t1.c t2.c)`。

**MESSAGE 指令的语法是：**\
&emsp;&emsp;`MESSAGE([SEND_ERROR | STATUS | FATAL_ERROR] "message to display" ...)`\
&emsp;&emsp;这个指令用于向终端输出用户定义的信息，包含了三种类型: \
&emsp;&emsp;&emsp;&emsp;`SEND_ERROR`，产生错误，生成过程被跳过。\
&emsp;&emsp;&emsp;&emsp;`SATUS`，输出前缀为—的信息。\
&emsp;&emsp;&emsp;&emsp;`FATAL_ERROR`，立即终止所有 cmake 过程.

## 4. 基本语法规
1. 在本例我们使用了`${}`来引用变量，这是 cmake 的变量应用方式，但是，有一些例外，比如在` IF `控制语句，变量是直接使用变量名引用，而不需要`${}`。
2. `指令(参数 1 参数 2...) `参数使用括弧括起，参数之间使用空格或分号分开。
3. 指令是大小写无关的，参数和变量是大小写相关的。但，推荐你全部使用大写指令。

## 5. 内部构建与外部构建
&emsp;&emsp;以编译 `wxGTK` 动态库和静态库为例，在 `Everest` 中打包方式是这样的：\
&emsp;&emsp;解开 `wxGTK` 后。\
&emsp;&emsp;在其中建立 `static` 和 `shared` 目录。\
&emsp;&emsp;进入 `static` 目录，运行`../configure –enable-static;make` 会在 `static` 目录生成 `wxGTK` 的静态库。\
&emsp;&emsp;进入 `shared` 目录，运行`../configure –enable-shared;make` 就会在 `shared` 目录生成动态库。\
&emsp;&emsp;这就是外部编译的一个简单例子。


## 注：
1. 比如 `SET(SRC_LIST main.c)`也可以写成`SET(SRC_LIST “main.c”)`是没有区别的，但是假设一个源文件的文件名是 `fu nc.c`(文件名中间包含了空格)这时候就必须使用双引号，如果写成了 `SET(SRC_LIST fu nc.c)`，就会出现错误。

