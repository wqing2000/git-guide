# git忽略上传文件&文件夹

## .gitignore配置文件

- [Git - gitignore 文档](https://git-scm.com/docs/gitignore)

可以用.gitignore来忽略我们不想提交到git上的文件。

```.gitignore
# 过滤整个文件夹
/mtk/   

# 过滤所有.zip文件
*.zip
# 过滤所有.DS_Store文件
*.DS_Store

# 过滤某个具体文件
/mtk/do.c

target/
.classpath
.project
.settings/
.springBeans
.metadata/
*.ipr
*.iws
*.iml
.idea/
.idea
../.idea/
*.swp
*.swo
*.swn

logs
```

- 配置语法：
	- 以斜杠“/”开头表示目录
	- 以星号“*”通配多个字符
	- 以问号“?”通配单个字符
	- 以方括号“[]”包含单个字符的匹配列表
	- 以叹号“!”表示不忽略(跟踪)匹配到的文件或目录；
	- 此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；

## 删除已上传文件/文件夹

已经被tracking 的文件或文件夹，再之后修改.gitignore 配置，还是会被提交。需要解除文件或文件夹的tracking 的状态。

1\. 第一步想到的让然是在这个文件里加上我要屏蔽的文件夹，
譬如：xxx/
只这样做，忽略的文件修改了仍会提交修改。

2\. 删除git的缓存。

如果 `git` 已经commit了某些想忽略的文件，这时候只在文件里加上想忽略的文件夹是不能生效的。可以理解成 有缓存，需要我们自己手动删除已经commit的文件，执行如下命令：
` git rm -r --cached ignoreFile`（`ignoreFile就是你想忽略的文件`），让`git`不再**tracking**这些文件。

```bash
git rm -r --cached .obsidian/workspace.json
```

提交修改到仓库

3\. 上面的**2步都需要执行**


# 参考

- [删除GIT中的.DS_Store · Issue #18 · nodejh/nodejh.github.io](https://github.com/nodejh/nodejh.github.io/issues/18)