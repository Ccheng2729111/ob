[[typescript 练习]]   [[typescript teach talk]]
## 所有类型的层级关系
首先需要了解所有类型的层级关系，比如never,any,unknow等等类型的层级，谁是谁的父级，谁是谁的子级。因为在日常的类型推倒，类型演算的时候，这个关系很值重要
- 类型之间的并集`|` 会向上取顶部的类型，即`never|'a'=>'a'`  `unknow | 'a' => unknow`
- 类型之间的交集`&` 会向下取底部的类型，即`never & 'a' =>never` `unknow & 'a' => 'a'`

最底层的类型是never 最顶层的类型是unknown 又是最顶层又是最底层的类型any![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2b639e1765924e39a439b87831966c5d~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)
### never 
是其他任意类型的子类型的类型成为底部类型
再typescript中，never类型是空类型和底部类型，never类型的变量无法被赋值，与其他类型求交集为自身，求并级不参与运算。
```typescript
interface IProps{
	a:string
	b:number
	c:()=>void
	d:()=>void
}

type GetKeyByValueType<T,C>={
[K in keyof T] : T[K] extends C ? K : never
}[keyof T]

// 演算过程
// 开始
{
    a: string
    b: number
    c: (e: MouseEvent) => void
    d: (e: TouchEvent) => void
}
// 第一步，条件映射
{
    a: never
    b: never
    c: 'c'
    d: 'd'
}
// 第二步，索引取值
never | never | 'c' | 'd'
// never的性质
'c' | 'd'

```

### unknown
指的是不可预先定义的类型，再很多场景下，可以代替any的功能同时也保留静态检查的功能

通常它的使用场景是，在避免使用any的情况下导致的静态类型检查的BUG
再我们无法确认的函数参数或者返回值类型的时候，使用unknown的场景会比较多