# git初始化

##### **初始化**

* `git init [dir]` 从本地初始化

* `git init --bare [dir]` 创建本地裸库

* `git clone <git-url> [dir]` 从远程仓库初始化

* `git clone [--branch tag-name/branch-name] <git-url> [dir]` 下载并绑定指定分支

* `git clone --bare <git-url> [dir]` 克隆远程仓库裸库

* `git clone --mirror <git-url> [dir]` 创建镜像仓库

* `git remote set-url <remote-host-name> <new-git-url>` 修改远程仓库地址

* 本地仓库初始化

  ```bash
  mkdir example
  cd example
  git init
  git remote add origin git@gitlab.com:trensy/cheatsheet.git
  #拉取远程分支
  git pull origin master 
  #推送数据到远程分支，如果远程分支不存在则创建同名远程分支
  git push -u origin master 
  ```

* 创建本地裸库

  ```bash
  mkdir example.git
  cd example.git
  git init --bare .
  ```

* 推送到新远程仓库(1)

  ```bash
  git clone --bare git@gitlab.com:trensy/cheatsheet.git
  git remote add origin git@gitlab.com:trensy/cheatsheet_new.git 
  git push --mirror origin
  ```

* 推送到新远程仓库(2)

  ```bash
  git clone --mirror git@gitlab.com:trensy/cheatsheet.git
  git remote update
  git remote add origin git@gitlab.com:trensy/cheatsheet_new.git
  git push --mirror origin
  
  ```

* 修改远程仓库地址

  ```bash
  git remote set-url origin git@gitlab.com:trensy/cheatsheet.git
  ```