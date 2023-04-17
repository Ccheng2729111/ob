#project #react #react-native 
react-native环境的问题有很多，一般要分情况，比如自己的环境是否是跟教程的环境一致，ruby,node,pod等是否相同。[[rn，配置，环境，初始化的坑]]

react-native打包现在是通过metro进行打包。现在的打包机制一般都是通过修改metro.config.js文件，在特定API中，也就是hook中进行添加相关的函数进行操作。
[[react-native打包原理，分包实践]]