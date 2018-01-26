# git提交记录——强迫症救星！

## 前言
进入自己github主页会看到自己的提交记录，如果某天没有提交记录，那天的小方框就显示灰色。强迫症的我，每次进来看着就感觉不爽，
想着自己每天记得提交点东西，争取像[阮一峰](https://github.com/ruanyf)大神一样，每天都有提交记录。  

![阮一峰git提交记录](./assets/git-commits.png "阮一峰git提交记录")

但是，毕竟是人，哪天忙了就会忘记提交，所以想着能不能实现在自己阿里云服务器上，设置cron，定制下git命令，实现每天定点自动提交。

## 第一步：克隆我的项目

不同的克隆方式导致校验方式不同，对应的免秘方式也不一样。简单来说，https通过记住账号密码免登，ssh通过校验生成的密钥免登。  
1. https克隆

![https克隆](./assets/https.png "https克隆")  

2. ssh克隆

![ssh克隆](./assets/ssh.png "ssh克隆")

如果，你已经克隆了项目，不知道采用了哪种方式，可以执行：
```bash
git remote -v
```
如果是这样：  

origin https://github.com/tywei90/git-auto-commit.git (fetch)  
origin https://github.com/tywei90/git-auto-commit.git (push)  

那么就是https方式； 

如果是这样：  

origin	git@github.com:tywei90/git-auto-commit.git (fetch)  
origin	git@github.com:tywei90/git-auto-commit.git (push)  

那么就是ssh方式；  

更改克隆方式也很简单：  

https ——> ssh  
git remote set-url origin git@github.com:tywei90/git-auto-commit.git  

ssh ——> https  
git remote 
set-url origin https://github.com/tywei90/git-auto-commit.git  

## 第二步：免密登录
针对上面两种克隆项目的方式，有两种免密登录设置。

### 1.账号密码免登（https克隆）
```bash
cd git-auto-commit/.git
vim config
```
在config文件最后添加如下代码：
```
[credential]  
    helper = store
```
保存，输入一次账号密码后第二次就会记住账号密码了

### 2.公钥私钥免登（ssh克隆）

#### <1> 生成公钥和私钥

检查本机的ssh密钥：
```bash
cd ~/.ssh 
ls
```
如果提示：No such file or directory，说明你是第一次使用git，那就自己手动创建目录  

使用ssh-keygen命令生成ssh密钥，命令如下：
```bash
ssh-keygen -t rsa
```
输入上面命令后，遇到选择直接回车，即可生成ssh 密钥。生成ssh 密钥后，可以到~/.ssh目录下查看相关文件，一般来说ssh 密钥会包含id_rsa和id_rsa.pub两个文件，分别表示生成的私钥和公钥。

#### <2>.拷贝公钥到你的github
在.ssh目录下，执行`cat id_rsa.pub`，复制所有公钥内容

点击github的头像，在下拉菜单中选择 setting 选项，在打开页面的左侧菜单中点击 SSH and GPG keys，然后点击新页面右上角绿色按钮 New SSH key。填写title值，并将复制的公钥内容粘贴到key输入框中提交。








