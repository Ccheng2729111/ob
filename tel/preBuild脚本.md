#node #Permanent #done

其实不算难，就是用node得环境对文件进行操作，比如文件的压缩，创建，读取，获取命令参数等等内容，其中有几个知识点[[process]] [[createReadStream]] 等等

有一些经验，对文件进行操作的时候，比如读取文件或者写入文件的时候可以使用流来创建或者读取。
```
// 创建读取流
const readStream = process.createReadStream(path)

// 创建写入流
const writeStream = process.createWriteStream(path)
```

这样比直接用fs对文件操作的好处是

1.  内存使用更加高效：使用流读取文件时，文件会被分成一个个小块（chunk）进行读取，并且每个chunk都会被单独处理，而不是一次性将整个文件读取到内存中。这意味着在读取大文件时，不会占用过多的内存，从而避免了内存溢出的风险。
    
2.  速度更快：流操作文件可以逐步地读取和处理数据，与一次性将整个文件读取到内存中然后再进行处理相比，它可以更快地将数据传输到另一个流或管道中。
    
3.  更好的可读性和可维护性：使用流操作文件可以将数据处理分为一系列小的步骤，每个步骤都可以单独处理。这使得代码更加可读和易于维护。
    
4.  更好的控制：使用流操作文件时，可以通过控制流的速率来控制数据的传输速度，这有助于避免数据被过度消耗或被处理太快而导致的问题。

然后使用了这么几个模块

1. path 获取文件路径信息用
2. fs 操作文件
3. archiver 压缩文件
4. crypto 获取文件的md5编码 
5. rimraf 递归删除文件以及文件夹

经验
- 在写脚本的时候如果对node的一些i/o的API了解比较熟悉的话 写起来应该比较顺畅
- 在写一些i/o的操作的时候需要注意同步，异步的顺序不能乱，需要对事件循环比较了解，有一些可能需要去包裹成一个promise
- 按照一步一步去拆分方法会比较好一些，比如第一步获取参数，第二步查看路径，第三步 创建json 第四步 压缩文件。按照这些步骤去写对应的方法，最后组合在一起。这样看起来思路清晰，流程明朗。 
