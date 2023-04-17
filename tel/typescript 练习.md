#fleeting #pendding #typescript 

```tsx
type Myreadonly<T>={
  readonly [P in keyof T] : T[P]
}

interface TODO{
  title:string
  description:string
}

const todoObj:Myreadonly<TODO> = {
  title:"hi",
  description:'demo'
}

todoObj.description = '1'

type First<T extends any[]> = T extends [] ? never : T[0]

type arr1 = ['a','b']
type arr2 = [1,2]
type arr3 = []

type head1 = First<arr1>
type head2 = First<arr2>
type head3 = First<arr3>

type TupleToObject<T extends readonly any[]> = {
  [P in T[number]] : P
}

const tuple = ['tesla','model 3'] as const
type result = TupleToObject<typeof tuple>

type Length<T extends unknown[]> = T['length']

type tesla = ['1','2','3']
type spaceX = [1,2,3,4,5,6,7]

type teslaLength = Length<tesla>
type spaceXLength = Length<spaceX>

type MyExclude<T,U> = T extends U ? never : T

type MyAwaited<T> = T extends PromiseLike<infer R>? MyAwaited<R> : T

type ExampleType = Promise<Promise<string>>

type Results = MyAwaited<ExampleType>

type IF<C extends boolean,T,K> = C extends true ? T : K
type A = IF<true,'a','b'>

type Concat<T extends any[],U extends any[]> = [...T,...U]

type Include<T extends any[],U> = U extends T[number] ? true:false

type ss = Include<['1','2'],'2'>

type Push<T extends any[],U> = [...T,U]

type pp = Push<[1,2],3>

type Unshift<T extends any[],U> = [U,...T]

type IParameters<T extends (...arg:any[])=>any> = T extends (...args:infer R)=>any?R:never

const foo = (arg1:number,arg2:string):void=>{}

type par = IParameters<typeof foo>

type MyReturnType<T> = T extends (...args:any[])=>infer R ? R : never

const fn = (v:boolean)=>{
  if(v) return 1
  return 2
}

type re = MyReturnType<typeof fn>

type deForTODO = keyof TODO

type MyOmit<T,U> = {
  [key in Exclude<keyof T,U>]:T[key]
}

type ReadOnly2<T,K extends keyof T = keyof T> = {
  readonly [P in K] : T[P]
} & {
  [P in Exclude<keyof T,K>] : T[P]
}

type DeepReadOnly<T> = T extends Function ? T : {
  readonly [K in keyof T]: T[K] extends Object ? DeepReadOnly<T[K]>: T[K]
}

const demo = {
  x:{
    a:'name',
    b:"age"
  },
  y:123
}

type dd = DeepReadOnly<typeof demo>

type Last<T extends unknown[]> = T extends [...unknown[],infer R] ? R :never
```

### 技巧

-   T[number] 用于获取数组的值，返回一个联合类型
-   P in T 用于获取一个联合类型中的一个，遍历联合类型
-   如果需要倒推返回值的类型，可以使用泛型的模式。 Chainable Options 12题
-   Awaited如果传入的是一个对象并且是带有promise特性，也就是有then方法的话，Promise.all 20题
-   106 type lookup 利用枚举的extends约束类型到{type:T}，如果符合就直接返回U就行
-   108 Trim Left 一样的利用extends 然后用别名类型infer，T进行判断，如果符合前面有特定的字符或者空格，就继续递归，如果不符合代表前面已经没有特殊符号或者空格了，直接返回别名就行