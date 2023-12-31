1. 规则需要与待校验的对象里的属性对应，由此衍生出一个问题，当待检验的数据是如下结构时

```ts
interface SourceData {
  name?: string;
  age?: number;
}
const sourceData: SourceData = {};
const validations = {
  name: { required, $autoDirty: true },
  age: { required, $autoDirty: true },
};
```

类型校验不会通过，因为 `vuelidate` 认为你的校验规则中含有 `name` 和 `age`，那么待校验的数据就必须存在这两个属性，但是实际场景中，大部分属性都是 optional 的，所以需要写一个方法，把 `sourceData` 转化成如下

```ts
const sourceData: SourceData = {
  name: undefined,
  age: undefined,
};
```

自己写了一个方法，但是没有进一步验证，算是一个 TODO

```ts
import useVuelidate, { ValidationArgs, ExtractState } from '@vuelidate/core';
import { ref, Ref } from 'vue';

/* eslint-disable @typescript-eslint/no-explicit-any */
export default function useCustomVuelidate<
  T extends {},
  Vargs extends ValidationArgs = ValidationArgs,
  EState extends ExtractState<Vargs> = ExtractState<Vargs>
>(validationsArgs: Vargs, state: T | Ref<T>) {
  const resultObject: Ref<{ [key in keyof Vargs]: any }> = ref({}) as Ref<{
    [key in keyof Vargs]: any;
  }>;

  // 确保响应性
  const stateRef = ref(state);
  for (const propertyName in validationsArgs) {
    if (Object.prototype.hasOwnProperty.call(validationsArgs, propertyName)) {
      resultObject.value =
        stateRef.value[propertyName] !== undefined
          ? stateRef.value[propertyName]
          : undefined;
    } else {
      resultObject.value[propertyName] =
        stateRef.value[propertyName] !== undefined
          ? stateRef.value[propertyName]
          : undefined;
    }
  }

  return useVuelidate(validationsArgs, resultObject, {
    $autoDirty: true,
  });
```

2. 计算规则的三种方法：
   - 手动调用 `$.touch`
   - 可以将值直接绑定到 `$model` 上，当值改变的时候，会自动调用 `$.touch`
   - 将 `autoDirty` 设置为 `true`, 会监听值的改变。推荐[全局设置](https://vuelidate-next.netlify.app/advanced_usage.html#returning-extra-data-from-validators)

## Example

```js
import { useVuelidate } from "@vuelidate/core";
import { required } from "@vuelidate/validators";

export default {
  setup: () => ({ v$: useVuelidate() }),
  data() {
    return { name: "" };
  },
  validations() {
    return {
      name: { required, $autoDirty: true },
    };
  },
};
```

**对于数组类型的数据仅支持简单的情况，较为复杂或使用 `withMessage` 的情况不适用**

```js
// 处理数组类型的的数据
const rules = {
  collection: {
    $each: helpers.forEach({
      name: {
        required,
      },
    }),
  },
};
```

## Custom

```js
import { required, helpers } from "@vuelidate/validators";

const validations = {
  name: {
    required: helpers.withMessage("This field cannot be empty", required),
  },
};
```
