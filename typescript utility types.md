---
date created: 2023-04-24 15:04
date updated: 2023-04-24 15:57
---

### Awaited Type

对promise的方法类型操作，对async的function进行await调用，返回promise的.then()。着重需要说的是 它会递归的去执行promise并且获取其返回

```js
type A = Awaited<Promise<string>>
// string
type B = Awaited<Promise<Promise<number>>>
// number
```

### Partial

将传入的type中所有的子级都转换成非必传的类型

```js
type A = {
	name:string 
	age:number
}

type B = Partial<A>
//{
//name?string 
//age?:number
//}

```

### Required

将对象中所有类型转换成必传类

```js
interface Props {

a?: number;

b?: string;

}

const obj: Props = { a: 5 };

const obj2: Required<Props> = { a: 5 };

Property 'b' is missing in type '{ a: number; }' but required in type 'Required<Props>'.
```

### Readonly

将对象中所有类型转换成只读类型

```js
interface Todo {

title: string;

}

const todo: Readonly<Todo> = {

title: "Delete inactive users",

};

todo.title = "Hello";

Cannot assign to 'title' because it is a read-only property.
```

### Record Keys Type

创建一个新的类型，key是传入传入的第一个枚举，可以是一个联合类型，value是传入的第二个类型

```js
interface  CatInfo {
	age:number 
	breed:string 
}

type CatName = 'A' | 'B' | 'C'

Record <CatName,CatInfo> = {
A:{age:number,breed:string}
}
```

### Pick Type Keys

创建一个新的类型 从第一个type中获取key对应是keys的子集的对象的数据

```js
interface  CatInfo {
	age:number 
	breed:string 
}

type CatName = 'age'

Pick <CatName,CatInfo> = {
age:number
```

### omit Type Keys

创建一个新的类型，从第一个type中去除掉key是第二个类型的子集的对象的类型

```js
interface  CatInfo {
	age:number 
	breed:string 
}

type CatName = 'age'

Omit <CatName,CatInfo> = {
bread:string
```

### Exclude UnionType ExcludeMembers

从联合类型中去除掉相应的子成员并且返回一个新的类型

```js
type T0 = Exclude<"a" | "b" | "c", "a">;

type T0 = "b" | "c"

type T1 = Exclude<"a" | "b" | "c", "a" | "b">;

type T1 = "c"

type T2 = Exclude<string | number | (() => void), Function>;

type T2 = string | number
```

### Extract Type Union

从两个联合类型中取出交集的元祖类型并且返回一个新的类型

```js
type T0 = Extract<"a" | "b" | "c", "a" | "f">;

type T0 = "a"

type T1 = Extract<string | number | (() => void), Function>;

type T1 = () => void
```

### NonNullable Type

从传入的类型中去除掉null或者undefined类型并且返回一个新的类型

```js
type T0 = NonNullable<string | number | undefined>;

type T0 = string | number

type T1 = NonNullable<string[] | null | undefined>;

type T1 = string[]
```

### Parameters type

从函数中获取传入的参数的元祖类型并且返回这个元祖类型

```js
declare function f1(arg: { a: number; b: string }): void;

type T0 = Parameters<() => string>;

type T0 = []

type T1 = Parameters<(s: string) => void>;

type T1 = [s: string]

type T2 = Parameters<<T>(arg: T) => T>;

type T2 = [arg: unknown]

type T3 = Parameters<typeof f1>;

type T3 = [arg: { a: number; b: string; }]
```

### ConstructorParameters Type

获取函数的构造函数的参数的元祖类型并且返回这个元祖类型

```js
type T0 = ConstructorParameters<ErrorConstructor>;

type T0 = [message?: string]

type T1 = ConstructorParameters<FunctionConstructor>;

type T1 = string[]

type T2 = ConstructorParameters<RegExpConstructor>;

type T2 = [pattern: string | RegExp, flags?: string]

type T3 = ConstructorParameters<any>;

type T3 = unknown[]
```

### ReturnType Type

获取函数的返回数据的类型并且返回这个类型

```js
declare function f1(): { a: number; b: string };

type T0 = ReturnType<() => string>;

type T0 = string

type T1 = ReturnType<(s: string) => void>;

type T1 = void

type T2 = ReturnType<<T>() => T>;

type T2 = unknown

type T3 = ReturnType<<T extends U, U extends number[]>() => T>;

type T3 = number[]

type T4 = ReturnType<typeof f1>;

type T4 = { a: number; b: string; }
```
