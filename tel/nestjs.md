#node #fleeting #pendding 


nestjs的设计模式就是典型的[[MVC]] 

nest日志可以用自带的winston进行记录。在入口main.ts先进行注册。

```jsx
const logger = WinstonModule.createLogger({
	level:'info',
	format:winston.format.json()
	transports:[
		new windston.transports.Console()
		new winston.transports.File({filename:'error.log',level:'error'})
	]
})

app.uselogger(logger)
```

全局错误捕捉，异常过滤器中可以使用Winston进行记录，全局异常过滤器可以使用

```jsx
@Module({
	imports:[]
	controllers:[AppController]
	providers:[
	{
		provide:APP_FILTER,
		useClass:ALLExceptionsFilter
	}
]
})
```

在nestjs中比如提供一个service模块，或者引入外部的service模块都需要进行模块的导入，可以在app.module.ts中全局导入也可以在自己的模块局部导入。如果是自己的service模块也需要在provider中引入，不然是不生效的。
