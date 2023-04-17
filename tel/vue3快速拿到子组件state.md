#fleeting #vue #done 
1.  子组件需要把需要传递的值用`defineExporse`包裹
2.  父组件引用子组件的时候 用ref进行定义
3.  定义的时候可以用子组件需要传递的ts类型进行定义，方便父组件引用数据

如果子组件不是setup的模版文件的话 父组件在使用子组件实例拿state的时候可以用`InstanceType`
直接获取类型
