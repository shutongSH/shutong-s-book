### 什么是 new

> `new` 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例。

**构造函数如果返回原始值，那么返回值毫无意义。但是如果返回值为对象，那么这个返回值会被正常使用**

```ts
function Far(name: string) {
    this.name = name;
    reutrn { age: 12 };
}
const far = new Far('car') // { age: 12 }
function Bar(name: string) {
    this.name = name;
    reutrn 12;
}
const bar = new Bar('car') // Bar { name: 'car' }
```
