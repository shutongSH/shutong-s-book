### Normal M0de

> 任何模式下，`ESC` 可切换至该模式

- h – 将光标向左移动一个字符。
- l – 将光标向右移动一个字符。
- k – 将光标向上移动一行。
- j – 将光标向下移动一行。
- w – 向后跳一个单词。
- b – 向前跳一个单词。
- 0 – 跳到行首。
- $ – 跳到行尾。

### Insert M0de

>

- i – 将 vim 置于插入模式，无论光标在哪里。
- a – 将光标移动到当前字符之后并进入插入模式。
- o – 在当前行下方插入新行并在新行上进入插入模式。
- Shift+I – 将光标移动到行首并进入插入模式。
- Shift+A – 将光标移动到行尾并进入插入模式。
- Shift+O – 在上方插入新行并在新行上进入插入式。

### Command M0de

> `:` 可切换至该模式

- :w – 保存文件
- :100 – 跳转到第 100 行
- / – 搜索
  > n - 正向搜索下一个
  > N - 反向搜索下一个

### Visual M0de

> 正常模式下 `v/V/CTRL+v`可进入可视模式

- v – 高亮显示文本光标所在的字符。
- Shift + V – 高亮显示整行。
- d – 删除高亮显示文本。
- y – 复制高亮显示文本。
  o
  ![VIM 操作图](ASSERTS/IMG/vim.jpg)
