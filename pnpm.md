#node 

在于解决了两个大的问题
### 磁盘空间

简单来说就是不用每个项目内是封闭的空间，以前用[[npm]] [[yarn]] 的时候会在项目的node_module中安装以来，如果是很多项目都用同一个版本的同一个依赖的话，那么占用的空间就是x10。
而pnpm会先把以来下载到自己的仓库`~/.pnpm-store`中，之后，会在真实的项目的`node_module`中创建一个模块的[[硬链接]]
如果在某个项目内用pnpm安装依赖的话 会从全局的store中找，如果有的话直接创建一个硬链接 指向磁盘中的某个文件。

### 幽灵依赖

在之前的[[npm]] 安装依赖的时候，会把所有的依赖打平放在`node_module`下面，这样会导致你可以引用到你压根没有安装的依赖（可能是你安装的依赖安装的三方依赖）

### pnpm workspace 

首先要启用workspace的话需要根目录下有`pnpm-workspace.yaml`配置文件，并且需要在其中指定工作空间的目录。比如
```yaml
packages:
	- 'packages/*'
```

其他的一些关于workspace的相关命令
```
// 安装全局的公共依赖
pnpm install react - w
// 安装全局的公共开发依赖
pnpm install rollup -wD
// 给某个package单独安装指定依赖
pnpm --filter "@babel/core" test  
pnpm --filter "@babel/*" test  
pnpm --filter "*core" test
// 运行某个package的命令
pnpm --filter <package_selector> <command>
// 模块之间的相互依赖
pnpm install @xx/monorepo2 -r -filter @xx/monorepo1 
```

### 文档思考
pnpm 相比于yarn有天然的workspace的优势，因为本身就会在全局的目录下创建.pnpm-store 文件夹并且在里面添加公共依赖，如果判断当前运行的目录下有workspace的文件就直接在当前文件的根目录下创建.pnpm-store 文件夹去管理公共依赖，而这恰好是work space的需求。