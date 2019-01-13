---
title: 配置ssh将本地仓库提交到github仓库
date: 2018-08-13 15:28:40
tags: ["git","ssh"]
categories: ["其他"]
---

# 配置ssh
## 配置账号和密码

```bash
$ git config --global user.name "myUsername" //配置你的账户名字
$ git config --global user.email "myEmail" //配置你的创建github账户的邮箱
```

配置完成后，可通过以下命令查看配置的结果
```bash
$ git config user.name
$ git config user.email
```
<!--more-->

显示结果
> myUserName  
myEmail

## 生成ssh文件
使用git bash控制台，输入以下指令：
```bash
$ ssh-keygen -t rsa -C "myEmail"
```
注：myEmail输入你实例的github邮箱！！！
创建完成之后，显示以下信息。提示你输入文件名，如果你在本机有多个ssh，则输入你指定的名称，若为空，则使用默认名称`id_rsa`
> Generating public/private rsa key pair.  
Enter file in which to save the key (/c/Users/wa02827/.ssh/id_rsa):

创建完成后，我们在个人用户目录`c/Users/wa02827(当前登录名，不同用户会有不同的文件夹)/.ssh`下看到`id_rsa`(私钥)和`id_rsa.pub`(公钥)两个文件。

## 在github上配置公钥
使用记事本打开你要上传的公钥（本例：`id_rsa.pub`)，内容如下：
>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC5Ez0jbSECncu+SzUDjc/JIzwco9hVg62kYcCIocpYnazn98pK5/fI1wJ/M8nogDwIjX9/u74qSLLojGNhAwuwuEEDjGUS8R6kR+Hn9tlUsLoARyJIfSiy9PUSqQX5RwowN9q0QAuDipGVZVnOzHLIdNccaJ06zTgWPxv+JyrB+Bu6GuXujlDvKWGE6gUpTE4fFA6rQp+KCRAdE1cboxiGSLo2xZ5xSiATK6gw61N1J2LeFAsecH8CSYKltPTYwIPfA2e7a/+U916ZRlQXKiKLCDmfdHCzL4h0g6BAMK304/k81k7DAVNCRLcIiNyP7KAvNJFXlq08e+984DkiwrMt

在github上，Settings->SSH and GPG keys点击`New SSH Key`按钮，将`id_rsa.pub`公钥数据复制到Key文本框，保存完成。

## 修改配置文件（单机器多个ssh重点）
检查用户/.ssh目录下，是否有config文件，若是没有，新建名称为`config`的文件(注：该文件没有文件类型后缀)。  编辑文件，添加以下内容：

>##别名，github默认为：github.com  
>Host github_wu.com  
>##数组名称  
>HostName github.com  
>##账号  
>User git  
>PreferredAuthentications publickey  
>##指定私钥文件，默认为~/.ssh/id_rsa  
>IdentityFile ~/.ssh/id_rsa.wu  

`~/.ssh/id_rsa.wu`为生成ssh时，个人指定的文件路径，默认名称为`~/.ssh/id_rsa`。

## 测试ssh
使用一下命名，测试ssh是否可用
```
$ ssh -T -V git@github_wu.com
```
成功显示如下：
> Hi tangname! You've successfully authenticated, but GitHub does not provide shell access.

实际使用的时候，例如Clone仓库，这可以使用以下命令
```bash
$ git clone git@github_wu.com:tangname/myblog.git
```
默认为 
> git@github.com:tangname/myblog.git

以上信息中，`tangname`为个人的github用户名，`myblog.git`为仓库名称。

# 配置本地仓库和远程仓库关联
若是直接通过`git clone`命令获取远程仓库，默认会添加关联。这里给出本地仓库先创建，而远程仓库还是空的时候，如何将本地仓库关联到远程仓库。

此处省略在github创建仓库步骤。

若远程仓库有文件(readme.md等)，首选获取远程仓库，命令如下：
注：若是远程仓库为空，该步可以省略
```bash
$ git pull
```
然后将获取的文件提交到本地仓库
```bash
$ git add *
$ git commit -m '提示消息'
```
添加关联
```bash
$ git remote add origin git@github.com:tangname/myblog.git
```
注：若是ssh配置了别名，则按配置的别名使用，例如使用 一、4、修改配置文件的配置，则命令如下：
```bash
$ git remote add origin git@github_wu.com:tangname/myblog.git
```
查看已配置的远程仓库
```bash
$ git remote
```
列表显示`origin`，表明该远程仓库已经关联成功。

然后执行命令，将本地仓库推送到远程仓库:
```bash
$ git push origin master
```
其中，`origin`为远程仓库别名，`master`为远程仓库中的分支名称。

至此，所有步骤完成。

