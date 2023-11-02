### 参考文献

[Types vs. interfaces in TypeScript](https://blog.logrocket.com/types-vs-interfaces-typescript/)

### Differences

1. Primitive types.
   `interface` 不能声明一种原始类型，只能声明对象类型
2. Union types.
   `interface` 不能声明联合类型
3. Function types.
   两者有细微差别

```ts
type AddFn = (num1: number, num2: number) => number;
interface IAdd {
  (num1: number, num2: number): number;
}
```

4. `interface`不能实现条件类型
5. Declaration merging.
   `interface` 可以实现声明合并

```ts
interface Client {
  name: string;
}
interface Client {
  age: number;
}
const harry: Client = {
  name: "Harry",
  age: 41,
};
```

6. Extends vs. intersection.
   `interface` 可以通过 `extends` 关键字来继承；`type` 可以通过 `&` 来合并类型

- `interface` 只能继承静态的已知类型

7. Handling conflicts when extending.
   `interface`不允许有相同的 property
   `type` 会将类型整合
8. implementing classes using interfaces or type aliases.
   class 两者都可以实现，但不可以实现联合类型
9. Working with tuple types.
   `type` 支持 tuple 类型
   `interface` 虽然不支持，但是可以通过其他方式实现

```ts
interface ITeamMember extends Array<string | number> {
  0: string;
  1: string;
  2: number;
}

const peter: ITeamMember = ["Harry", "Dev", 24];
const Tom: ITeamMember = ["Tom", 30, "Manager"]; //Error: Type 'number' is not assignable to type 'string'.
```

10. Advanced type features.
    `type` 有更加丰富的功能：条件类型、泛型类型、类型保护、高级类型
