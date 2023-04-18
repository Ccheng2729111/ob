#feeting #node 
这API是创建一个标准的读取流，用于创建一个可读流的对象，用于从文件中读取数据。这个函数可以接受一个文本路径作为参数（那这个是不是跟[[readFile]]差不多 只不过是创建的是一个 [[node中流的概念]] ）返回一个可读流的对象，通过这个对象可以读取制定文件的内容。

```javascript
const fs = require('fs')

const stream = fs.createReadStream('path/to/file.txt')
stram.on('data',(chunk)=>{
	console.log(chunk.toString())
})
```
上面的代码中，我们使用 `createReadStream` 函数创建了一个可读流对象 `stream`，并指定了要读取的文件路径。接着我们监听了 `stream` 对象的 `data` 事件，在事件回调函数中将读取到的数据块转换成字符串并输出到控制台。

`createReadStream` 函数还支持一些可选参数，例如 `start` 和 `end`，用于指定读取文件的起始和结束位置。另外还可以指定 `highWaterMark` 参数，用于控制读取数据的缓冲区大小。

同样的createWirteStream是一样的概念，创建一个写文件的的对象，返回一个写取的流，并且可以进行后续流的操作。