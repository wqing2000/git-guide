# 配置SSH密钥

## 背景

代码管理 （Codeup）的仓库支持 HTTP(S) 和 SSH 两种访问协议，SSH 协议可以实现安全的免密认证，且性能比 HTTP(S) 协议更好。

- 获取远程仓库的代码有两种方式：
  - https：每一次和远程仓库通信都需要用户名和密码。
  - ssh : 生成两个秘钥，将公钥给匹配的网站，私钥放置在本地。

- 克隆远程仓库代码时，选择的[远程仓库的地址](远程仓库的地址.md "远程仓库的地址")不同，使用上
- 如果选择 ssh 的方式拉取代码库，需要配置ssh密钥。

## 前提条件

在使用 SSH 协议操作代码库前，请生成并上传你的 SSH 公钥，完成 SSH 公钥和远程仓库(如：github)账号的对应。

通过 SSH 协议访问 Codeup，需要满足如下条件。

- 本机已安装 Git（安装教程参见[安装Git](https://help.aliyun.com/zh/yunxiao/user-guide/install-git#topic-2405645)）并保证版本大于 1.9（通过`git --version`可获取本地的版本）。
    
- 本机需要安装 OpenSSH 客户端（GNU/Linux, macOS, 或 Windows 10 已内置 OpenSSH）。
    
- SSH 尽量保持最新，6.5之前的版本由于使用 MD5 签名，可能存在安全问题。
    

**重要**

如果你是 Windows 用户，在使用 Git 命令时，请**使用** [**WSL**](https://docs.microsoft.com/en-us/windows/wsl/install)**（需要Windows10或以上），或使用** [**Git Bash**](https://gitforwindows.org/)。

SSH 加密算法类型如下所示：

| 算法类型        | 公钥             | 私钥         |
| ------------- | -------------- | ---------- |
| ED25519（推荐) | id_ed25519.pub | id_ed25519 |
| RSA（不推荐)    | id_rsa.pub     | id_rsa     |



## 步骤一：查看已存在的 SSH 密钥

在生成新的 SSH 密钥前，请先确认是否需要使用本地已生成的SSH密钥，SSH 密钥对一般存放在本地用户的根目录下。

```bash
# ED25519 算法
cat ~/.ssh/id_ed25519.pub

# RSA 算法
cat ~/.ssh/id_rsa.pub
```

## 步骤二：生成 SSH 密钥

注释会出现在`.pub`文件中，一般可**使用邮箱作为注释内容**。

```bash
# 基于`ED25519`算法，生成密钥对命令
ssh-keygen -t ed25519 -C "<注释内容>"

# 基于`RSA`算法，生成密钥对命令
ssh-keygen -t rsa -C "<注释内容>"
```

输入命令后，点击回车，选择 SSH 密钥生成路径。

> [!WARNING] 警告
> 密钥用于鉴权，请谨慎保管。公钥文件以 .pub 扩展名结尾，可以公开给其他人，而没有 .pub 扩展名的私钥文件不要泄露给任何人！

---

5. 确认您的 SSH 密钥是否正确生成，并且公钥（public key）已添加到您的 GitHub 账户。
   [[配置ssh]]
6. 使用 ssh-add 命令将密钥添加到 SSH 代理中。运行以下命令：

## 步骤三：拷贝公钥

除了在命令行打印出已生成的公钥信息手动复制外，可以使用命令拷贝公钥到粘贴板下，请参考操作系统使用以下命令进行拷贝：

```bash
# Windows系统 copy
cat ~/.ssh/id_ed25519.pub | clip

# Mac系统 copy
tr -d '\n' < ~/.ssh/id_ed25519.pub | pbcopy
```

### macOS 系统，查看ssh公钥。

```shell
### 进入.ssh目录
cd ~/.ssh

### 查看文件的内容，2种不同的密钥(加密算法不同)，用其中一种即可
cat ~/.ssh/id_rsa.pub
cat ~/.ssh/id_ed25519.pub
```

将密钥添加到钥匙串：

```bash
ssh-add -K ~/.ssh/id_ed25519
# 添加到系统 keychain
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

确认您的 SSH 密钥是否正确生成，并且公钥（public key）已添加到您的 GitHub 账户。

```bash
ssh-add -l
```



# 摘录

SSH密钥有以下作用：

• 认证用户身份，允许用户安全地登录到远程服务器。

• 实现无需输入密码的登录，提高安全性并简化访问过程。

• 加密数据传输，确保信息在互联网上的安全性。

• 允许自动化和脚本化操作，提高效率并减少人为错误。


# 参考

- [如何配置SSH密钥-阿里云帮助中心](https://help.aliyun.com/zh/yunxiao/user-guide/configure-ssh-key)
- [如何在同一台电脑上配置多个SSH Key？-阿里云帮助中心](https://help.aliyun.com/document_detail/322237.html)
