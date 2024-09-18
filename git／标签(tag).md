# 标签(tag)

* `git tag` 查看标签

* `git tag <tag-name>` 创建命名标签

* `git tag -a <tag-name> -m <message>` 添加一个注解标签

* `git tag <tag-name> <commit-id> -a -m <message>` 给过去提交记录创建标签

* `git push origin <tag-name>` 推送标签到远程仓库

* `git push origin --tags` 推送全部标签

* `git pull origin --tags` 远程拉取标签

* `git tag -d <tag-name>` 删除本地标签

* `git push origin :refs/tags/<tag-name>` 删除远程标签