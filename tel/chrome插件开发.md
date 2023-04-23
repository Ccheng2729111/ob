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
background这个API可以方便我们在后台jing mo