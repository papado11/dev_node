# file

## 文件描述符

文件描述是非负整数。打开现存或新建文件是，系统（内核）会返回一个文件描述符。文件描述符用来指定已打开的文件。  
在系统调用（文件IO），文件描述符对文件起到标识作用，如果要操作文件，就是对文件描述符的操作。  
但一个层序运行或者一个进程开启时，系统会自动创建三个文件描述符。

- `#define STDIN_FILENO 0`&ensp;&ensp;stdin&ensp;&ensp;标准输入  
- `#define STDIN_FILENO 1`&ensp;&ensp;stdout&ensp;&ensp;标准输出  
- `#define STDIN_FILENO 2`&ensp;&ensp;stderr&ensp;&ensp;标准错误输出  

如果自己打开文件，会返回文件描述符，而文件描述符一般按照从小到大依次创建的顺序。

## open函数

man 2 open > a.txt

```cpp
#include <errno.h>      // perror函数的头文件
#include <fcntl.h>      // open函数的头文件
#include <sys/stat.h>   // open函数的头文件
#include <sys/types.h>  // open函数的头文件
#include <unistd.h>     // close函数的头文件

#include <iostream>

int main(int argc, char const *argv[]) {
  using namespace std;
  /**
   * @brief 第一个参数是文件陆路经 第二个参数为打开方式
   * 当第二个参数有创建文件的操作时，第三个参数表示创建文件的权限 一个程序最多能创建1024个文件描述符。
   */
  int fd = open("c.txt", O_RDONLY);

  if (-1 == fd) {  // 打开失败的时候
    cout << "errno: " << errno << endl;
    perror("fail open c.txt");  // 输出错误信息
    return -1;
  }

  cout << "fd: " << fd << endl;
  close(fd);

  return 0;
}
```
