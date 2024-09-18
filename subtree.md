# subtree

* `git subtree add --prefix=<sub-repository-path> <sub-git-url> master [--squash]` 在父仓库中新增子仓库

* `git subtree pull --prefix=<sub-repository-path> <sub-git-url> master [--squash]` 拉取更新子仓库

* `git subtree push --prefix=<sub-repository-path> <sub-git-url> master` 推送子仓库

* 给子仓库添加远程仓库,方便复用子仓库git仓库地址

  ```bash
  git remote add -f <sub-remote-git> <sub-git-url>
  git subtree add --prefix=<sub-repository-path> <sub-remote-git> master
  ```