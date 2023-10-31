## 场景

1. 当多人开发时，很容易造成 pnpm-lock file conflicts, 对 code merge 造成困扰
2. 当开发时，为了方便很多包的版本都是时间戳的形式(`0.2023.10110253`)，而测试开始时需要一个 fixed version，也希望把这个固定版本的过程自动化起来

## 动手

**这个过程需要用到两个文件：`dep-version.json`、`package.json`。一般来讲需要设置成 dynamic 的 dependencies，需要将`package.json` 的版本设置成约定好的字符，然后根据字符将`dep-version.json`里的版本设置成对应的版本号**

```json
package.json
...
"dependencies": {
    "@target-client": "",
}
...
```

```json
dep-version.json
{
    "resolutions": {
        "@target-client": "0.2023.10110253",
    }
}
```

### 第一步。识别`package.json`里的空版本，并从`dep-version.json`拿到正确的版本号

```ts
import path from 'path';
import { readFile } from 'fs-extra';
import findUp from 'find-up';
export type DepVersionsBase = {
  enableDynamic?: boolean;
  resolutions: {
    [key: string]: string;
  };
};

async function readDepVersionsFile() {
    try {
        const lockfilePath = await findUp('pnpm-lock.yarm');
        const filepath = path.join(lockfilePath, '..', 'dep-version.json');
        const content = (await readFile(filepath)).toString();
        const depVersion: DepVersionsBase = JSON.parse(content);
        return depVersion
    }
}
```

### 特殊情况：CUT 前需要将版本号改为 CUT version
