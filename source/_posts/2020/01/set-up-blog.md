---
title: 利用Github+Hexo搭建博客网站
p: 2020/01/set-up-blog
date: 2020-01-15 16:05:06
tags: 
categories:
---
<!--
 * @Descripttion: 利用Git+Hexo搭建个人博客
 * @Author: Lewin Cheng
 * @Date: 2020-01-15 16:05:06
 * @LastEditors  : Lewin Cheng
 * @LastEditTime : 2020-01-15 17:39:07
 -->
 
## 注册GitHub并创建Repository
1. 填写**username**，注册成功。
2. 点击右上角'+'：New repository
3. Repository name：**username**.github.io（即博客地址）
4. 选择Public
5. Create repository

## 安装Git
- Windows：https://git-scm.com/download/win
- Mac：使用Homebrew, MacPorts 或下载安装程序安装
```shell
sudo brew install git
```

## 安装Node.js
- http://nodejs.org/

## 配置与github的连接
- 配置Git环境
```bash
cd username.github.io
# 配置用户名密码
git config --global user.name "username"
# user.email为github邮箱
git config --global user.email"username@example.com"
```
- 在Git Bash下
```bash
# 添加这台机器对github的ssh权限；生成密钥
ssh-keygen -t rsa -C "user@mail.com"
# 进入.ssh文件夹：
cd c:
cd /c/users/user/.ssh---隐藏文件夹
# 将生成的密钥添加到 ssh-agent
ssh-add id_rsa
````
- 在GitHub中Setting进行公钥上传。将id_rsa.pub中公钥全部复制添加到SSH公钥。
```bash
# 测试，出现以下代码代表连接成功
ssh -T git@Github.com
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```
- 在用户根目录下找到`.gitconfig`文件，添加以下信息
```
[user]
    name = username
    email = username@example.com
```

## 安装Hexo
- 用Git Bash进入需要放置仓库的本地盘（如：D盘）
```bash
# 创建本地仓库：初始化的过程是从 hexo 仓库下载博客的目录结构和文件
hexo init username.github.io
# 或者将创建好的Repository拷贝到本地
# git clone git@github.com:username/username.github.io.git
# 安装Hexo
npm install -g hexo-cli
# 安装依赖模块
npm install
npm install hexo-deployer-git
```

## 建站
- 打开`username.github.io`目录下的`_config.yml`文件，在文件中底部添加如下配置信息：
- 进行测试
- 备份与发布  
在Github上新建分支`hexo`用来备份博客源文件，`master`备份网站源文件
    - 在hexo分支下
    ```bash
    # 将必要的文件依次添加
    git add .
    # 备注信息
    git commit -m "add valine and live2d"
    # push到Github项目的hexo分支上
    git push -u origin hexo
    ```
    - 在master分支下
    ```bash
    # 清除缓存
    hexo clean
    # 生成本地发布文件夹
    hexo g
    # hexo deploy：部署
    hexo d
    ```
## 新建博客文章
```bash
# 生成.md的文件。source/_posts
# hexo new post postname
# 指定路径生成post，如2020/01
hexo new post -p 2020/01/postname
# 生成草稿，但不会存在于静态网页中。source/_draft
hexo new draft draftname
```

## 注意事项
`hexo init`会初始化Hexo环境，该操作会清空`.git`文件夹，导致版本控制信息会丢失。  

因此除了首次搭建环境之外，无需运行此命令。  

如果万不得已出现 Hexo 环境损坏，需要重新初始化，可以先拷贝出 `.git`文件夹，然后搭建环境并初始化之后，将`.git`信息重新拷贝回来。