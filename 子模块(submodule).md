# 子模块(submodule)

##### **子模块(submodule)**

* `git submodule add <sub-git-url> <sub-repository-path>` 添加子模块

* `git submodule foreach git pull [remote-host-name] [remote-branch-name]` 更新

* `git clone <git-url> --recursive` clone 主库和子模块

* `git submodule init` 初始化本地配置文件

* `git submodule update` 检出父仓库列出的commit

* 更新整个仓库

  ```
  git pull
  git submodule init && git submodule update // or git submodule update --init --recursive 
  git submodule foreach git pull origin master // 更新代码时使用
  ```

* 删除子仓库(sub-repo)

  ```
  git rm --cached sub-repo
  rm -rf sub-repo
  删除 .gitmodules 文件 [submodule "sub-repo"] 相关内容
  删除 .git/config 文件 [submodule "sub-repo"] 相关内容
  ```