# 彻底删除git中的大文件

git 如果提交一个文件，然后删除他，继续提交，那么这个文件是存在 git 中，需要使用特殊的命令才可以删除。

```txt
.git主要记录每次提交变动，当我们的项目越来越大的时候，我们发现 .git文件越来越大

很大的可能是因为提交了大文件，如果你提交了大文件，那么即使你在之后的版本中将其删除，但是，
实际上，记录中的大文件仍然存在。

虽然你在后面的版本中删除了大文件，但是Git是有版本倒退功能的吧，那么如果大文件不记录下来，
git拿什么来给你回退呢？但是，.git文件越来越大导致的问题是： 每次拉项目都要耗费大量的时间，并且每个人都要花费
那么多的时间。。

git给出了解决方案，使用git branch-filter来遍历git history tree, 可以永久删除history中的大文件，达到让.git文件瘦身的目的。
```

```bash
# 列出git仓库中，占用空间最多的5个文件
git rev-list --objects --all | grep "$(git verify-pack -v .git/objects/pack/*.idx | sort -k 3 -n | tail -5 | awk '{print$1}')"

# 列出所有仓库中的对象（包括SHA值、大小、路径等），并按照大小降序排列，列出TOP 10。
git rev-list --all | xargs -rL1 git ls-tree -r --long | sort -uk3 | sort -rnk4 | head -10
```

1\. 使用 git filter-branch 命令从 Git 历史中删除大文件:

```bash
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch path/to/大文件名' --prune-empty --tag-name-filter cat -- --all
```

2\. 更新 .gitignore 文件,防止该文件再次被提交。

3\. 清理 Git 仓库:

```bash
rm -Rf .git/refs/original
rm -Rf .git/logs/
git gc --aggressive --prune=now
```

4\. 强制推送更改到远程仓库:

```bash
git push origin --force --all
```

5\. 如果需要删除 Git LFS 中的文件,可以使用:

```bash
git lfs uninstall
```