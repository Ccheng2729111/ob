#fleeting #node #pendding


### 原理
在运行的时候会检测你的==yarn.lock pnpm-lock.yaml package-lock.json== 以了解当前的包管理器，并运行相应的命令。
这里就就要说一下[[yarn]] [[pnpm]] [[npm]] [[npx]] 
也就是说它会根据你当前项目内的lock文件来判断应该运行哪个命令，这样就可以避免在一个项目内使用不同的包管理的命令导致依赖混乱
如果没有锁文件，默认就会让用户选择 [[npm]] [[yarn]] [[pnpm]]. 然后执行相应的命令。这里可以在`~/.nirc
文件中设置全局的默认配置，就可以默认走对应的命令
### 使用

1. 安装依赖
```
ni 

# npm install
# yarn intall
# pnpm install
```
2. 运行命令
```
nr dev --port=3000
```
3. nx 执行命令
```
nx jest
nx react-native init xxxx
```


### 源码

	package.json文件

```
{
    "name": "@antfu/ni",
    "version": "0.10.0",
    "description": "Use the right package manager",
    // 暴露了六个命令
    "bin": {
        "ni": "bin/ni.js",
        "nci": "bin/nci.js",
        "nr": "bin/nr.js",
        "nu": "bin/nu.js",
        "nx": "bin/nx.js",
        "nrm": "bin/nrm.js"
    },
    "scripts": {
        // 省略了其他的命令 用 esno 执行 ts 文件
        // 可以加上 ? 便于调试，也可以不加
        // 或者是终端 npm run dev \?
        "dev": "esno src/ni.ts ?"
    },
}
```

	ni.ts

```js
// ni/src/runner.ts
export async function runCli(fn: Runner, options: DetectOptions = {}) {
  // process.argv：返回一个数组，成员是当前进程的所有命令行参数。
  // 其中 process.argv 的第一和第二个元素是Node可执行文件和被执行JavaScript文件的完全限定的文件系统路径，无论你是否这样输入他们。
  const args = process.argv.slice(2).filter(Boolean)
  try {
    await run(fn, args, options)
  }
  catch (error) {
    // process.exit方法用来退出当前进程。它可以接受一个数值参数，如果参数大于0，表示执行失败；如果等于0表示执行成功。
    process.exit(1)
  }
}
```

关于[[process]] ，node的api。