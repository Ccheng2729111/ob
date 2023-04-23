#feeting #done 
最主要的是manifest.json。里面可以配置例如版本，描述，插件程序的版本，弹窗依赖的html,js。设置插件的快捷方式弹出。
但是popup这种只能做一些临时的交互操作。用完就关闭了，没法存储信息或者其他标签页的交互等等。这个时候就需要background，它是一个常驻的页面。生命周期是插件中所有的类型页面的中最长的，随着浏览器打开而打开，关闭而关闭。通常把需要一直运行的，启动就运行的，全局的代码放在background里面。 


```javascript
// 插件安装时运行
chrome.runtime.onInstalled.addListener(callback)

// 同步设置全局数据，获取全局数据
chrome.storage.sync.set(data,callback)
chrome.storage.sync.get(data,callback)
```

开发插件的话不在乎用的是什么framework，无论用react，vue还是什么，只要有html就可以当做chrome的插件去开发。
background这个API可以方便我们在后台静默的去干一些事情，比如爬虫爬数据，比如请求数据，在开新的tab的时候去从storage里面获取新的数据即可。
如果是使用react或者vue开发chrome的插件的话，需要注意的是几个点
- chrome本身这个api在framework的dev环境是没有的，可以考虑安装@type/chrome的类型定义，帮助我们在开发环境去使用代码提示
- chrome本身是没有的，我们可以使用window.chrome去规避eslint的提示，或者在.eslintrc文件里面定义一下全局变量chrome
- 像bckaground这样的文件是纯js，只有在扩展里面才会启用，可以写在public里面，每次调试需要打包后使用
- 如果要使用es6的语法的话 需要注意你的manifest.json的version是几，如果是3的话没问题 不用做额外的处理，如果是2的话需要对语法进行转换，转换成es5甚至更低，去兼容低版本的浏览器。
- background这个，是存在休眠期的，如果需要唤醒可以使用特定的api，alarm，在长轮询的时间去做特定的事情，比如拉去新的数据或者爬取某个网站的数据进行展示
- 使用framework进行开发好处我觉得是可以使用现代化的开发方式去开发chrome插件，代码结果，代码风格，使用习惯，三方依赖等问题可以很好的解决 


### content script和background script的区别
content script主要用于向页面注入javascript css的那个资源，可以与网页上已经有的DOM进行交互，实现动态操作，可以获取和修改浏览器窗口中打开的网页的状态，可以响应页面事件，例如加载，点击按钮或者填写表单等等。但是需要注意的是不能够直接访问chrome.extension api等其他的浏览器的API

background script则是整个插件的生命周期内只存在一个实例化的对象的javascript代码，用于扫描webrequest监听网络请求，处理一些后台逻辑，执行周期任务等等，主要是负责管理和响应extension浏览器API的请求，并且维护一些全局的状态数据。相比而言，背景脚本更加强大，可以访问chrome浏览器API中的全部功能，包括存储，tab页面等等的控制

