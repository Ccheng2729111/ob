---
date created: 2023-04-24 15:04
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
从元祖类型中去除掉相应的子成员并且返回一个新的类型
```js
type T0 = Exclude<"a" | "b" | "c", "a">;

type T0 = "b" | "c"

type T1 = Exclude<"a" | "b" | "c", "a" | "b">;

type T1 = "c"

type T2 = Exclude<string | number | (() => void), Function>;

type T2 = string | number
```

### Extract Type Union
从两个元祖类型中取出交集的元祖类型并且返回一个新的类型
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

### ParameTers 