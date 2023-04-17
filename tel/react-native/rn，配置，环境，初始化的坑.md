#project #react #react-native #env

#### js爆栈,maxstack等
这里需要注意安装@react-native 脚手架的时候的node版本需要跟你react-native init，初始化项目的时候的版本要一致，否则会有问题，我现在用的16.19.x版本没问题

### 环境配置流程
1.  安装xcode
2.  更新ruby到2.7.6，因为ios这边rn的编译底层靠的是ruby，所以需要更新ruby到rn指定的版本
    1.  安装ruby需要用包管理器RVM，这里需要注意先安装gnupg来安装公钥，这是安装RVM的前置动作`brew install gnupg`
    2.  随后运行`gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB`
    3.  curl网站安装命令`\\curl -sSL [<https://get.rvm.io>](<https://get.rvm.io/>) | bash -s stable`
    4.  `source ~/.bashrc source ~/.bash_profile` 将环境命令生效一下即可安装不同版本的ruby
3.  通常情况下直接按照官网运行 `npx react-native init demoApp`肯定会在安转依赖，安装cocoapods或者各种情况下报错，所以这边推荐只是初始化项目但是不安装依赖，运行 `npx react-native init DemoApp --skip-install` 跳过安装步骤，自己手动安装
4.  进入项目根目录运行`npm install`安装package.json中的依赖，用于跑scripts。这里需要注意node版本和npm的版本不能太低。
5.  安装cocoapods，`gem info cocoapods` 这里需要用ruby的依赖管理工具来安装，使用brew安装的pod没法用，目前看来是这样
6.  cd ios/ 到iOS目录下面运行`pod install --verbose --no-repo-update` 安装ios build需要的依赖
    1.  这里可能需要很久很久，没有其他的版本，用镜像/挂梯子都一样的，并且中间可能会从git上拉不下来依赖报错，总之遇到报错就重新运行命令安装，一直到最后整个安装结束。
7.  最后pod install安装结束后 打开ios目录下的DemoApp.xcworkspace 用xcode进行build ios。build过程中如果报错是端口被占用，参考这篇文档操作[](https://zhuanlan.zhihu.com/p/53038329/)[https://zhuanlan.zhihu.com/p/53038329/](https://zhuanlan.zhihu.com/p/53038329/)

其他的小tips

-   `npx react-native doctor` 查看当前项目环境是否正常，可以根据输出的信息修改对应缺失的地方
-   `npx react-native info` 查看当前你的运行环境，包括各种依赖的版本，可以看自己的依赖版本是否跟别人的对应的上
-   如果遇到了一些未知的问题，比如ruby的版本问题，node的问题，react-native cli的问题，最好的办法就是删除依赖重新安装依赖，不然这些问题很难去解决

npx react-native bundle --entry-file index.js --platform ios --dev false --bundle-output ios/main.jsbundle --assets-dest ios