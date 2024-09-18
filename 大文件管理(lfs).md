# 大文件管理(lfs)

在 Git 仓库中，通常认为超过 100MB 的文件就算是大文件。Git 本身并不是为处理超大文件而设计的，因此管理大文件可能会遇到一些问题，如克隆时间长、存储空间浪费、文件太大无法提交到远程仓库(视使用的远程仓库而定)等。

---

**Git LFS (Large File Storage)**:

Git LFS 是一款 Git 扩展，它专门用于管理大文件。通过 Git LFS，你可以将大文件的实际内容存储在外部服务器，而仓库中仅保存指向这些大文件的引用。这可以大幅减少仓库的大小。

开启 Git LFS 的步骤：

```bash
git lfs install
git lfs track "*.psd"  # 例如要跟踪 .psd 文件
git add .gitattributes
git add <大文件>
git commit -m "Add large file using Git LFS"
git push origin <你的分支>
```

通常来说，有大文件应该使用网盘或OSS 来存储。亦或分隔成小文件再存储到git中（这个要慎用，免费存储**超级多**的文件，可能会封号）

--- 

* `git lfs track "<pattern-file-name>"` 跟踪需要处理哪些文件

  ```bash
  #追踪所有后缀为a的文件
  git lfs track "*.a"
  ```

* `git lfs ls-files` 可以显示当前被lfs追踪的文件列表

* `git lfs track` 查看现有的文件追踪模式

* `git lfs untrack "*xx.a"` 取消git fls对xx.a的追踪管理

* `git lfs version` 查看当前所用git lfs版本

* `git lfs pull` 从远程仓库拉取大文件

* 安装

  ```bash
  #详细见
  https://github.com/git-lfs/git-lfs#downloading
  ```