# commit type规范

* `feat: ` 新功能（feature）

* `fix: ` 修补bug

* `docs: ` 文档修改（documentation）

* `style: ` 代码格式修改，不影响代码运行的变动

* `refactor: ` 重构（即不是新增功能，也不是修改bug的代码变动）

* `test: ` 增加测试

* `chore: ` 构建过程或辅助工具的变动

### git commit message

Git 每次提交代码，都要写 Commit message（提交说明），否则就不允许提交。

```bash
$ git commit -m "hello world"
```

上面命令的`-m`参数，就是用来指定 commit mesage 的。

如果一行不够，可以只执行`git commit`，就会跳出文本编辑器，让你写多行。

基本上，写什么都可以，但是，一般来说，commit message 应该清晰明了，说明本次提交的目的。

目前，社区有多种 Commit message 的写法规范。本文介绍[Angular 规范](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#heading=h.greljkmo14y0)（见上图），这是目前使用最广的写法，比较合理和系统化，并且有配套的工具。