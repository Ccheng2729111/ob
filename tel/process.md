#fleeting #node #done 

process对象是一个node的全局对象，提供当前node进程的信息可以在脚本的任意位置使用，不必通过require命令加载。该对象部署了[[eventEmitter]]接口。

## 属性
process对象用户提供一系列的属性，用于返回系统信息。
- process.argv 返回一个数组，成员是当前进程的所有命令行参数
- process.env 返回一个对象，成员为当前shell的环境变量，比如process.env.HOME
- process.installPerfix：返回一个字符串，表示安装路径的前缀，比如/usr/local
- process.pid：返回房钱进程的进程号
- process.title 返回一个字符串，默认为node，可以自定义
- process.version 返回当前node版本
- process.platform 返回当前的操作环境
### process.stdout
process.stdout 属性返回一个对象，表示标准输出。该对象的write方法等同于console.log，可以标准输出用户的显示内容
```
var fs = require('fs');

fs.createReadStream('wow.txt')
  .pipe(process.stdout);
```
上面的[[createReadStream]] 表示讲一个文件导向标准输出 也可以说一下[[node中流的概念]]
上面的代码中，由于process.stdout和process.stdin与其他进程的通信，都是流的形式，所以必须通过pipe管道命令中介
### process.stdin
返回一个对象，表示标准化输入。 

```javascipt
process.stdin.pipe(process.stdout)
```
上面的代码表示读取用户标准化输入后再进行标准化输出

### process.stderr
表示标准化错误

### process.argv

属性返回一个数组，第一个总是node的绝对路径也，第二个是执行node命令的脚本的绝对路径，后面就是各个参数来进行组成

所以如果要获取命令的参数，直接用process.argv.slice(2)即可获取。

### process.execArgv

获取node可执行文件与脚本文件之间的命令的参数

## 方法

-   `process.chdir()`：切换工作目录到指定目录。
-   `process.cwd()`：返回运行当前脚本的工作目录的路径。
-   `process.exit()`：退出当前进程。
-   `process.getgid()`：返回当前进程的组ID（数值）。
-   `process.getuid()`：返回当前进程的用户ID（数值）。
-   `process.nextTick()`：指定回调函数在当前执行栈的尾部、下一次Event Loop之前执行。
-   `process.on()`：监听事件。
-   `process.setgid()`：指定当前进程的组，可以使用数字ID，也可以使用字符串ID。
-   `process.setuid()`：指定当前进程的用户，可以使用数字ID，也可以使用字符串ID。

process.cwd()和__dirname是有可能不一样的，如果当前是node的绝对路径 那么返回的是当前你运行命令的绝对地址，但是__dirname是你运行的文件的绝对路径

process.exit方法接受的参数如果大于0 表示执行失败，如果是0表示执行成功

process.on跟web端的window.addEventListen是一样的意思，监听某一个事件，然后运行回调即可。

如果node有错误throw的话 会默认退出当前进程，如果是监听了uncaughtException的话 不会退出当前进程。

如果使用process.stdin.resume() 获取用户标准话术入的话 会挂起当前线程