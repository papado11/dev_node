# shell

## bash 的特性

```shell
history # 命令历史记录
        # -c 清空历史记录
        # -r 回复历史记录
echo $HISTSIZE 
less ~/.bash_history
!历史id 这执行理事命令
!! 执行上一条命令
# ctrl+l 快速清屏
```

## 变量

* ' 单引号，不识别特殊语法
* " 双引号，能识别特殊符号
* \` 反引号，中的命令执行结果会被保留下来  ``name=`ls` ``

每次调用bash/sh解释器执行脚本，都会开启一个子shell，因此不保留当前的shell变量，通过调用source（或者点.符号，在当前shell环境加载脚本，因此保留变量

### 环境变量

环境变量一般指的是用expo内置命令导出的变量，用于定义sh刨的运行环境、保证sh酬命令的正确执行。shell通过环境变量确定登录的用户名、PH路径、文件系统等各种应用。

环境变量可以在命令行中临时创建，但是用户退出shell终端，变量即丢失，如要永久生效，需要修改`环境变量配置文件`。

* 用户个人配置文件`~/bash-profi1e～`、`/.bashrc`远程登录用户特有文件。
* 全局配置文件`/etc/profile`、`/etc/bashrc`，且系统建议最好创建在`/etc/profile.d/`，而非直接修改主文件，修改全局配置文件，影响所有登录系统的用户。

**检查系统环境变量的命令**  
* set，输出所有变量，包括全局变量、局部变量。
* env，只显示全局变量。
* declare，输出所有的变量，如同set。
* export，显示和设置环境变量值。

**撤销环境变量**  
* unset变量名，删除变量或函数。


**设置只读变量**
* readonly，只有shell结束，只读变量失效。

```shell
readonly name="what"
name="d"
# -bash: name: readonlyvariable
```

```shell
$? # 上一次命令的返回值 通常0是成功 1-255为失败
```

### 特殊变量

shell的特殊变量，用在如脚本，函数传递参数使用，有如下特殊的，位置参数变量。
* `$0` 获取shell脚本文件名，以及本路径。
* `$n` 获取shell脚本的第n个0数，n在1~9之间，如$1, $2,$9，大于9则需要写，\${10}，参数空格隔开。
* `$#` 获取执行的shell删本后面的参数总个数。
* `$*` 获取shell脚本所有参数，`"$*"`为单个字符串。
* `$@` 获取shell脚本所有参数，`"$@"`可迭代。

### 特殊状态变量

* `$？`上一次命令执行状态返回值，e正确，非0失败。
* `$$` 当前shell脚本的进程号。
* `$!` 上一次后台进程的PID。
* `$_` 一再次之前执行的命令，最后一个参数。

```shell
man bash # 搜索`specialParameters`
```

## bash一些基础的内置命令

```shell
echo hello # -n 不换行输出
           # -e 解析字符串中的特殊符号
                # \n换行
                # \r回车
                # \t制表符四个空格
                # \b退格
printf hello # 不换行输出
eval "ls;cd /etc" # 执行命令
exec "ls" # 不创建子进程，执行后续命令，且执行完毕后，自动exit
```

## shell子串的用法

`${param}` 返回变量值。  
`${#param}` 返回变量长度，字符长度。  
`${param:start}` 返回变量酐offset数值之后的字符。  
`${param:start:length}` 提取offset之后的length限制的字符。  
`${param#word}` 从变量开头删除最短匹配的word子串。  
`${param##word}` 从变量开头，删除最长匹配的word。  
`${param％word}` 从变量结尾删除最短的word。  
`${param％％word}` 从变量结尾开始删除最长匹配的word。  
`${param/pattern/string}` 用string代替第一个匹配的patter。   
`${param//pattern/string}` 用string代替所有的pattern。 

```shell
# 统计字符长度的方法
strr="hello"
wc # 统计命令
   # -l 统计行数。 -L统计最长的行的长度。
echo $strr | wc -l # 1
echo $strr | wc -L # 5

expr # 数值计算
expr length $strr # 5
echo ${#strr}

seq # 序列命令 -s 指定分隔符
seq -s "~" 10 # 1~2~3~4~5~6~7~8~9~10

time ls # 统计代码执行的时间
        #real实际运行时间 user用户态运行时间 sys内核态运行时间
```

## 条件判断

1. 基本语法  
   (1). test condition  
   (2). \[ condition \]（注意condition前后要有空格）  
   注意：条件非空即为true，\[atguigu\]返回true，\[ \]返回false。0为真值，非0为假，这与常见的编程语言不太一样。

2. 常用判断条件
   1. 两个整数之间的比较  
   -eq 等于(equal)  
   -lt 小于(less than)  
   -gt 大于(greater than)  
   -ne 不等于(not equal)  
   -le 小于等于（less equal)  
   -ge 大于等于(greater equal)  
   注：如果是字符串之间的比较，用等号“=”判断相等；用“!=”判断不等。
   2. 按照文件权限进行的判断
   -r 有读的权限(read)  
   -w 有写的杖限(write)  
   -x 有执行的权限(execute) 
   3. 按照文件类型进行判断  
   -e 文件存在(existence)  
   -f 文件存在并且是一个常规的文件(file)  
   -d 文件存在并且是一个目录(directory)  

3. 示例
```shell
[ -r hello.sh ] # 判断是否又可读的权限
echo $?

[ -r hello.txt ] && [ 1 = 2 ] 多条件判断
echo $?

[ 1 -eq 1 ] && echo OK || echo Not ok # 三元运算
# OK
```

# 流程控制

## if 判断

1. 基本语法
   1. 单分支
   ```shell
   if [ 条件判断式 ];then
        程序
   if

   
   if [ 条件判断式 ]
   then
        程序
   if
   ```
   2. 多分支
   ```shell
   if [ 条件判断式 ]
   then
        程序
   elif [ 条件判断式 ]
   then
        程序
   else
        程序
   fi
   ```
