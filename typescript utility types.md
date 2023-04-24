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
...
}
```
