## execa

地址：[npm](https://www.npmjs.com/package/execa)

> Process execution for humans
> 代替 `Node.js` 原生的`child_process` 模块
> 有更好的异步控制和异常处理机制

## commander

地址：[Github](https://github.com/tj/commander.js/blob/HEAD/Readme_zh-CN.md#commanderjs)

> 完整的`node.js`命令行解决方案

### API

一般使用 **`.option`** 来定义选项
`-`后面接单个字符，表示短选项名称
`--`后面接一个或多个单词，使用 `, 空格 ｜` 分隔
对于选项，一类是`boolean`类型的选项，选项无需配置参数，另一类选择则需要设置参数，使用尖括号声明在该选项后，如果在命令行中不指定该参数，则被定义为 `undefined`, 方框号声明的参数是 optional 的

### Examples

```js
const { Command } = require("commander");
const program = new Command();
program
  .option("--first", "display just the first substring")
  .option("-s, --separator <char>", "separator character", ",");
```

```shell
Options:
  --first                 display just the first substring
  -s, --separator <char>  separator character (default: ",")
```
