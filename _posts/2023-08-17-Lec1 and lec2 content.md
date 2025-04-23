---
layout: post
title:  "MIT missing Cour"
date: 2023-08-17
---

进度条…(2/8)

# Lecture 1 Shell

* bash中如果想提供一个包含空格的参数，可以用‘或"“把它们引起来，或者用转义字符\，比如My\ Photos来将空格转义

* `$PATH`是环境变量，即在本地文件夹下没有找到对应可以执行的程序时会自动在环境变量的路径中寻找相应的程序。`which`提示了能够运行本指令的程序路径，比如

   `~$ which echo /bin/echo `

* `ls -l`表示以详细方式列出当前文件夹下的文件

   `missing:~$ ls -l /home drwxr-xr-x 1 missing  users  4096 Jun 15  2019 missing `

   第1个字符表明这个文件的类型。d表示这是一个文件夹，如果是-表示这是一个普通文件，l表示这是一个链接文件，类似于windows下的快捷方式，b表示这是一个块设备文件，一般置于/dev目录下，没有文件大小，只有一个主设备号和辅设备号。块设备是一次传输一整块数据的设备，比如硬盘。c表示这是一个字符设备文件，一般置于/dev目录下，字符设备是一次只传输一个字符数据的设备，比如键盘。p表示这是一个命令管道文件，与shell编程有关，s表示这是一个socks文件，与shell编程有关

   d后面有3*3个标志，表示不同的身份对该文件的权限。r表示可读权限，w表示可写权限，x表示可执行权限，-表示无相应权限。第一组表示该文件的所有者的权限，第二组表示文件所有者同组用户的权限，第三组表示其他用户的权限

   权限后面的第一个数字表示1. 当这是一个文件时，为硬连接数，即有几个文件硬链接到了这个文件 2. 当这是一个文件夹时，为链接占用的节点，即该目录中包含的子目录的个数

   对于一个文件夹来说，为了进入这个文件夹，必须拥有"search"权限，也就是拥有对这个文件夹以及其所有父路径文件夹的x权限。为了`ls`这个文件夹，必须拥有这个文件夹的r权限

* **重定向输入输出流**：`< file`将输入设定为文件，`> file`将结果输出到文件，原先文件的内容会被覆盖

   `missing:~$ echo hello > hello.txt missing:~$ cat hello.txt hello missing:~$ cat < hello.txt hello missing:~$ cat < hello.txt > hello2.txt missing:~$ cat hello2.txt hello `

   `>>`可以来向文件附加数据。`|`是管道符号，可以将前一个命令的输出作为下一个命令的输入。

   `curl --head --silent google.com | grep --ignore-case content-length | cut --delimiter=' ' -f2 # 查看向google发送HTTP GET请求的头文件中的content length属性的值 `

   文件描述符：一般情况下每个unix命令运行时都会打开3个文件：

   * 标准输入文件(stdin)：文件描述符为0，unix默认从stdin输入数据
   * 标准输出文件(stdout)：文件描述符为1，unix默认向stdout输出数据
   * 标准错误文件(stderr)：文件描述符为2，unix会向stderr流中写入错误消息

   默认情况下，`command>file`将stdout重定向到file，`command<file`将stdin重定向到file

   `command 2>>file # 将stderr追加到文件末尾// `

   /dev/null文件是一种特殊的文件，写入到它的内容都会被丢弃，也无法从中读取到任何内容，如果希望执行某个命令，但是不希望在屏幕上显示输出结果，可以将输出重定向到/dev/null

   `command >> /dev/null 2>&1 # 屏蔽stdout和stderr `

   `command >> /dev/null`已经将标准输出重定向，`2>&1`中的`&`表示等同，`2>`表示错误输出，`2>&1`表示错误输出重定向的对象等同于标准输出重定向的对象，即`/dev/null`

* `sysfs`：Linux内核下基于内存的文件系统，可以将很多内核参数以文件形式暴露，从而可以方便地修改kernel。比如笔记本电脑的屏幕亮度可以以文件的形式在`sys/class/backlight`下被暴露

   `$ sudo find -L /sys/class/backlight -maxdepth 2 -name '*brightness*' /sys/class/backlight/thinkpad_screen/brightness $ cd /sys/class/backlight/thinkpad_screen $ sudo echo 3 > brightness  # permission denied，因为>重定向符号之前的sudo并不能被后面观察到，也就是说写入brightness这个操作实际上并没有执行sudo $ echo 3 | sudo tee brightness  # success，tee这个命令是获取标准输入，将内容输出成文件，并将其打印到屏幕上 `

* `chmod`(change mode)来控制用户对文件的权限的命令。只有文件拥有者(owner)和超级用户(super user)可以修改文件或者目录的权限

   `chmod [-cfvR] [--help] [--version] mode file... # mode格式为 [ugoa...][[+-=][rwxX]...][,...] # u表示该文件的拥有者，g表示与该文件的拥有者属于同一个group者，o表示其他人，a表示这三者皆是 # +表示增加权限，-表示取消权限，=表示唯一设定权限 # r表示可读取，w表示可写入，x表示可执行，X表示只有当该文件是个子目录或者该文件已经被设定过为可执行 # 示例:将file1.txt设定为所有人皆可读取 chmod ugo+r file1.txt `

   也可以采用八进制的方法来规定权限

   | #    | 权限         | rwx  | 二进制 |
   | ---- | ------------ | ---- | ------ |
   | 7    | 读+写+可执行 | rwx  | 111    |
   | 6    | 读+写        | rw-  | 110    |
   | 5    | 读+执行      | r-x  | 101    |
   | 4    | 只读         | r–   | 100    |
   | 3    | 写+执行      | -wx  | 011    |
   | 2    | 只写         | -w-  | 010    |
   | 1    | 只执行       | –x   | 001    |
   | 0    | 无           | —    | 000    |

   `# file1.txt这个文件对所有的用户均可读可写可执行 chmod 777 file1.txt # file2.txt这个文件对其他用户只可执行 chmod ug=rwx,o=x file2.txt # 与以下相同 chmod 771 fil2.txt `

   一般比较常用的是`chmod 755`和`chmod 777`

* shebang: `#!`

   写在脚本的第一行，用来规定该脚本的解释器。`#!`后接解释器的绝对路径。比如想要规定这个脚本用sh来执行，那么在第一行添加

   `#!/bin/sh `

   推荐使用`/usr/bin/env python`来规定该脚本解释器，这是因为`env`会在`$PATH`中查找python解释器的安装位置，这样可以不用提供一个解释器的绝对路径，从而提高程序的可移植性

* 后台执行shell

   在shell命令的最后一个位置加`&`

# Lecture 2 Shell Tools and Scripting

## Shell Scripting

Shell是一个用C语言编写的程序，是一种解释性语言。Windows Explorer是一个典型的图形界面shell

Bourne Shell /bin/sh或/usr/bin/sh

Bourne Again Shell /bin/bash

* 给变量赋值：

   注意在定义变量时变量名不加美元符号，变量名和等号之间不能有空格。在使用一个已经定义过的变量时需要加美元符号

   `foo=bar # 注意不能是foo = bar，否则bash会认为这是运行了foo命令，并以=和bar作为参数传入 echo "$foo" # prints bar echo '$foo' # or echo "${foo}" # 花括号加不加可选，主要是为了清晰变量名的边界 # prints $foo # 注意在bash中"和‘是不同的。在'中$变量不会被替换，"中$后面的变量会被替换为其值 `

   `readonly`变量是只读变量，不能被赋值

   `myurl="www.fanxiao.tech" readonly myurl `

   使用`unset`命令可以删除变量

* 获取字符串的长度

   `string="abcd" echo ${#string} # 输出4 `

* 提取子字符串

   从字符串的第2个字符开始截取四个字符

   `string="runoob is a great site" echo ${string:1:4} # 输出unoo `

* 函数

   `# 以shell脚本的名称创建一个文件夹并cd到这个文件夹中 mcd(){ mkdir -p "$1" cd "$1" } `

   * `$0`：脚本本身的名称
   * `$1`-`$9`：脚本的第1-第9个参数
   * `$@`：所有脚本的参数
   * `$#`：脚本参数的个数
   * `$?`：前一个命令的返回代码
   * `$$`：当前脚本的PID
   * `!!`：完整的上一个命令，包括参数。如果一个命令只是因为没有root权限失败，则可以执行`sudo !!`来重新执行该命令
   * `$_`：上一个命令的最后一个参数

* 数组

   数组索引从0开始。用括号()来表示数组，数组元素用空格分开。定义数组的一般形式为

   数组名=(值1 值2 值3 值4)

   如

   `array_name=(value0 value1 value2) `

   还可以单独定义数组的各个分量，如`array_name[0]=1`

   读取数组元素值的方式是`$(数组名[下标])`，使用`@`则可以获取数组中的所有元素，例如

   `echo ${array_name[@]} `

   获取数组的长度的方法是

   `length=${array_name[@]} `

* bash基本运算

   原生bash不支持简单的数学运算，但是可以通过其他命令实现，比如`expr`

   `val=`expr 2 + 2`   # 注意：表达式和运算符之间一定要有空格，例如2+2是不对的，必须写成2 + 2,注意不是单引号而是反引号 echo "两数之和为$val"  # 输出为"两数之和为4" `

   条件表达式要放在方括号之间，并且要有空格，例如

   `if [$a == $b] then echo "a等于b" fi if [$a != $b] then echo "a不等于b" fi `

   关系运算符：

   | 运算符 | 说明                                             |
   | ------ | ------------------------------------------------ |
   | -eq    | 检测两个数是否相等，相等则返回true               |
   | -ne    | 检测两个数是否不等，不等则返回true               |
   | -gt    | 检测左边的是否大于右边的，大于则返回true         |
   | -lt    | 检测左边的是否小于右边的，小于则返回true         |
   | -ge    | 检测左边的是否大于等于右边的，大于等于则返回true |
   | -le    | 检测左边的是否小于等于右边的，小于等于则返回true |
   | !      | 非运算                                           |
   | -o     | 或运算                                           |
   | -a     | 与运算                                           |

   注意：乘号前必须要加上反斜杠\转义才是乘法运算

* `test`命令可以用于检查某个条件是否成立

   `# 数值测试 num1=100 num2=200 if test $[num1] -eq $[num2] then echo '两个数相等' else echo '两个数不相等' fi # 文件测试 cd /bin if test -e ./bash then  echo '文件存在' else echo '文件不存在' fi `

   注意：新的test`[[]]`比旧的test`[]`更好，尽量使用`[[]]`

* 流程控制：shell编程的流程控制不可为空，即`if`和`else`的代码块里必须执行一定的动作

   将`if`和`else`写成一行的方法：

   `if [ $(ps -ef | grep -c "ssh") -gt 1]; then echo "true"; fi # 查找当前所有进程中ssh进程的个数，如果大于1则返回true `

   `for`循环的一般格式

   `for var in item1 item2 ... itemN do command1 command2 commandN done `

   写成一行：

   `for var in item1 item2 itemN; do command1; command2; commandN; done; `

   `while`循环：

   `int=1 while [ $int -lt 5 ] do echo $int let "int++"  # let是bash中用于计算的工具，变量计算中不需要加上$表示变量 done # 运行结果 # 1 # 2 # 3 # 4 # 5 `

   `case`选择

   每个case分支从右圆括号开始，用两个分号`;;`表示break，跳出整个`case...esac`语句

   `echo '输入1到4之间的数字' echo '你输入的数字为' read aNum case $aNum in 1) echo '你选择了1' ;; 2) echo '你选择了2' ;; 3) echo '你选择了3' ;; 4) echo '你选择了4' ;; *) echo '你没有输入1到4之间的任何数字' ;; esac `

   `break`命令

   `while true do echo -n "输入1到5之间的数字" read aNum case $aNum in 	1|2|3|4|5) echo "你输入的数字为$aNum!" 	;; 	*) echo "你输入的数字不是1到5之间的！结束" 		break        ;;    esac done `

* shell函数

   `[function] funname [()] { action [return int] } # example demoFun(){ echo "第一个shell函数" } demoFun # 调用这个函数 `

* 程序的返回值：执行成功返回0，执行失败则返回其他大小的数值。注意，和C语言不同，shell中0表示true，1表示false

   获取一个程序的变量值，如`$(CMD)`会先执行`CMD`，获取`CMD`的输出并再相应位置进行替换。比如执行`for file in $(ls)`，将先执行`ls`，然后遍历执行`ls`后获得的返回值

* 进程替换(process substitution)：`<(CMD)`将执行`CMD`，然后将结果输出到一个临时文件，并把`<()`替换为这个文件名。比如`cat <(ls -l)`相当于`ls -l | cat`，`diff <(CMD1) <(CMD2)`是比较这两个`CMD`的区别

* shell文件包含

   包含外部脚本，以封装一些公用的代码作为一个独立文件

   `. file # 注意.和文件名中间有一个空格 # 或者 source file `

* shell通配符(globbing)

   wildcard: 使用`*`或`?`来进行匹配，比如有`foo1`、`foo2`、`foo`几个文件，`rm foo?`将删除`foo1`和`foo2`，而`rm foo*`将删除`foo1`、`foo2`和`foo`等三个文件

* 花括号`{`用来扩展子字符串

   `convert image.{png,jpg} # will expand to convert image.png image.jpg`