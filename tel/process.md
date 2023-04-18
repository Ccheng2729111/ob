#fleeting #node #pendding 

process对象是一个node的全局对象，提供当前node进程的信息可以在脚本的任意位置使用，不必通过require命令加载。该对象部署了[[eventEmitter]]接口。

## 属性
process对象用户提供一系列的属性，用于返回系统信息。
- process.argv 返回一个数组，成员是当前进程的所有命令行参数
- process.env 返回一个对象，成员为当前shell的环境变量，比如process.env.HOME
- process.installPerfix：返回一个字符串，表示安装路径的前缀，比如/usr/local
- process.pid：返回房钱进程的进程号
- process.title 返回一个字符串，默认为node，可以自定义
- process.version 返回当前node版本