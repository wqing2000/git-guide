# 同一台电脑配置多个SSH Key

需要使用 ssh config 配置


已经在gitlab中输入了ssh keys id_ed25519 密钥，但是使用git clone 命令时，仍要求输入gitlab帐号密码是什么情况？

这种情况可能是由于以下几种原因引起的：
	1.	SSH密钥没有正确添加到GitLab账户：请确保你已正确添加密钥到GitLab账户。也可以检查本地的SSH private key与GitLab上的SSH public key是否匹配。
	2.	SSH-Agent没有运行：SSH-Agent负责管理SSH keys并提供访问已授权的key。你需要启动ssh-agent并添加你的私钥。在Linux或Mac上，可以运行以下命令：

```shell
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

	3.	Git仓库的URL是HTTPS而不是SSH：如果你在克隆时使用的URL是HTTPS而不是SSH，那么它会要求你输入用户名和密码。你可以在GitLab的仓库处找到适用于SSH的URL，它应该看起来像git@gitlab.com:username/repository.git。

	4.	SSH交互式方式受阻：SSH在连接时会尝试多种方式进行认证，包括交互式密码方式(interactive password authentications)。如果密码方式先于公钥方式被尝试或者SSH公钥方式失败了，系统可能会要求输入密码。编辑你的 ~/.ssh/config 文件，添加以下配置可以禁用密码方式：

```shell
Host gitlab.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_ed25519
```

	5.	本地SSH配置问题：检查在本地的 ~/.ssh/config 文件中是否有指定的IdentityFile或特殊的HostName。

请根据以上步骤尝试解决你的问题，如果这些步骤不能解决问题，可能需要查看更详细的错误信息。这可以通过运行 `GIT_SSH_COMMAND="ssh -v" git clone git@gitlab.com:username/repository.git` 来获取。



## 每次重启macos 都需要重新授权 git 获取 id_ed25519的权限
报错如下：
Enter passphrase for key '/Users/wangqing/.ssh/id_ed25519':
怎么配置永久权限？

MacOS 使用了一个叫作 ssh-agent 的程序来管理 SSH 私钥。每次你重启你的电脑时，你需要重新加载你的私钥到 ssh-agent。但是你可以设置你的 MacOS，在每次启动时自动加载私钥。
为了实现这个，我们需要在 ~/.ssh/config 文件中进行一些配置。下面是具体步骤：
	1.	打开 Terminal。
	2.	使用下面的命令打开 config 文件。如果它不存在，这个命令将会创建它。

```shell
vim ~/.ssh/config
```

	3.	如果你的 config 文件是空的，或者没有包含下面的内容，你需要添加它：
```yaml
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

这段配置的意思是：对于所有连接 (Host *)，我们告诉 ssh-agent 和 MacOS keychain 自动加载并记住 ssH 私钥 (AddKeysToAgent yes , UseKeychain yes)，并且使用你指定的私钥文件 (IdentityFile ~/.ssh/id_ed25519)。

	4.	保存并关闭文件。然后在 Terminal 中输入下面的命令，确认无误：

```shell
ssh-add -K ~/.ssh/id_ed25519
```

现在，不论你何时重启你的电脑，你都不需要再手动输入密码来让 ssh-agent 记住你的 SSH 私钥了。