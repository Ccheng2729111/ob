1.  `compilerOptions`

`compilerOptions`是最重要且最常用的配置项。它用于指定有关TypeScript编译器和输出结果的设置，可以设置许多不同参数。

例如：

-   `target`：目标低级 JavaScript 版本（如`ES5`, `ES6`, `ES2017`等）；
-   `module`：用来描述在代码生成阶段时如何处理模块的选项（如`CommonJS`, `ES6`, `AMD` 等）；
-   `outDir`：输出文件夹路径；
-   `sourceMap`：是否生成源码映射文件（可帮助在调试时定位错误的位置）；
-   `declaration`：是否生成类型声明文件（.d.ts 文件）；
-   `strict`：开启所有严格检查（包括 noImplicitAny, strictNullChecks, strictFunctionTypes 和 strictPropertyInitialization 等）。

2.  `include` 和 `exclude`

`include` 是一个数组，其中包含将被编译的文件或文件夹的相对或绝对路径。`exclude` 则是一个与之相反的数组，其中包含不应该被编译的文件和文件夹的相对或绝对路径。

例如：

json复制代码

`{   "include": ["src/**/*"],   "exclude": ["node_modules", "**/*.test.ts"] }`

上面的例子告诉 TypeScript 编译器只编译`src`文件夹下的所有文件，但排除了`node_modules`文件夹和所有 `.test.ts` 文件。

3.  `typeRoots`

`typeRoots`是一个指定类型定义文件的（根）文件夹列表。这些文件将不会经过具体模块解析而被直接引用。

例如：

json复制代码

`{   "typeRoots": [     "./typings",     "./node_modules/@types"   ] }`

上述例子中，TypeScript 将查找 `./typings` 和 `./node_modules/@types` 下的 `.d.ts` 文件来获取类型声明。

4.  `tsconfig.json` 继承

通过继承其他的 TypeScript 配置文件，在不同的开发、打包、测试环境下简化配置，也方便多人开发或管理琐碎的配置信息。

具体内容可以参考 TypeScript 官网文档：[在 tsconfig 中使用 extends](https://www.typescriptlang.org/tsconfig#extends)。

总之，以上列出的是几个常见的`tsconfig.json`的配置选项。如果您要按照具体项目的需求进行更改或添加，请确保先阅读相关官方文档，以确保代码的质量和稳定性。