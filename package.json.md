在package.json文件中，一些比较有用的属性如下：

1.  `name`: 项目名称，必填项。
2.  `version`: 项目版本号，必填项，使用“语义化版本控制”（Semantic Versioning）规范。
3.  `description`: 项目描述，可选项。
4.  `keywords`: 项目关键词数组，可选项。
5.  `repository`: 项目仓库地址及类型，可选项。
6.  `license`: 项目所采用的许可证，必填项。
7.  `author`: 项目作者信息，可选项。
8.  `contributors`: 项目贡献者信息数组，可选项。
9.  `main`: 项目主入口文件路径，可选项。
10.  `dependencies`: 项目生产环境依赖包和版本号信息，定义该属性的包会被安装到`node_modules`目录下，并在生产环境中被使用。
11.  `devDependencies`: 项目开发环境依赖包和版本号信息，定义该属性的包会被安装到`node_modules`目录下，并在开发环境中被使用。
12.  `scripts`: 定义常用的脚本命令，例如运行测试、构建等。
13.  `peerDependencies`: 项目对其他包的依赖信息，通常是为了提供插件或运行时库。
14.  `optionalDependencies`: 项目的可选依赖包信息。
15.  `engines`: 定义项目所需要的Node.js和npm引擎版本。
16.  `private`: 项目是否为私有包，如果设置为true，则不能上传至公共仓库。

以上属性是比较常用和重要的，还有一些其它可选的属性，在你构建自己的项目时可以根据实际情况进行设置。