# 0使用Git向阿里云code更新代码

## 一、创建并添加SSH  Keys

```shell
cat ~/.ssh/id_rsa.pub	//判断是否已经存在本地公钥
ssh-keygen -t rsa -C "flyerwge@163.com"		//生成ssh key
```

如果看到一长串以 `ssh-rsa`或 `ssh-dsa`开头的字符串，则为本地公钥；

复制这个公钥放到个人设置中的SSH/My SSH Keys下，完整拷贝从`ssh-`开始直到你的用户名和主机名为止的内容。

## 二、连接远程仓库并克隆所需代码

```shell
git init 	//初始化

git remote add origin git@code.aliyun.com:EMGAcquisition/USB.git	//连接远程仓库 origin可修改为远端对应分支
git clone 粘贴基于HTTPS或者SSH的地址

git checkout master    //获取master分支的最新更改
```

## 三、通过Git向阿里云code更新代码

```shell
git pull 远端 分支名称 	//(远端: origin) (分支名称: 可以是"master"或者是一个已经存在的分支) origin可修改为远端对应分支
git pull origin save	//拉取某分支的最新副本（建议工作时每次都输入这个命令）。

git checkout -b save	//在本地建立分支，在这个分支上进行修改
git add .	//添加所有文件
git commit -m "增加将数据存向数据库功能"	//将文件提交到仓库
git status	//查看

git push 远端 分支名称
git push origin save
git push origin save -f //强制push

git checkout .	//删除代码库的所有更改（不包含提交到暂存区的变更）
git clean -f	//删除代码库的所有更改（包含未跟踪的文件）

git checkout master
git merge 分支名称	//将某分支合并到master分支
```

