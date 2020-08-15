---
title: Hexo教程
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## 搭建步骤

**GitHub创建个人仓库**

仓库名应该为：用户名.github.io

**安装Git**

安装完git后，设置user.name和user.email配置信息，设置github与本地计算机的ssh密钥连接。

ssh设置完成后可通过如下命令验证是否设置成功

```bash
$ ssh git@github.com
```

**安装Node.js**

可直接在[官网](https://nodejs.org/en/)下载Node.js进行安装，官网网址

注意安装Node.js会包含环境变量以及npm的安装，安装后输入如下指令检测是否安装成功

```bash
$ node -v
```

```bash
$ npm -v
```

**安装Hexo**

使用npm命令安装Hexo

```bash
$ npm install -g hexo-cli
```

如果安装时间过长，可能是由于镜像在国外的原因，可以先切换淘宝镜像，然后再执行npm安装Hexo命令

```bash
$ npm config set registry http://registry.npm.taobao.org
$ npm install -g hexo-cli
```

如果是mac系统还可能遇到权限问题，需要开启root用户，然后使用root权限安装Hexo命令

开启方法见[Mac官网](https://support.apple.com/zh-cn/HT204012)  

```bash
$ sudo npm install -g hexo-cli
```

## 常用命令

### 初始化博客

```bash
$ hexo init [博客文件夹名]
```

### 新建博客

```bash
$ hexo new "博客名"
$ hexo n "博客名"  //简写
```

   More info: [Writing](https://hexo.io/docs/writing.html)

### 生成静态文件

```bash
$ hexo generate
$ hexo g //简写
```

More info: [Generating](https://hexo.io/docs/generating.html)

### 启动服务预览

```bash
$ hexo server
$ hexo s //简写
```

浏览器输入[http://localhost:4000](http://localhost:4000/)  ，即可预览博客页面

More info: [Server](https://hexo.io/docs/server.html)

### 部署博客到github上

```bash
$ hexo deploy
$ hexo d //简写
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)

### 清除缓存

```bash
$ hexo clean
```

## Hexo部署目录本地同步

### 将hexo目录从本地更新到github

**未上传到github过**

1. 先执行hexo deploy，将网页静态文件部署到github上去

2. 在github的chunyangzhao.github.io版本库中创建hexo分支(分支名可自定义)，用于存放hexo目录

3. 下载chunyangzhao.github.io版本库，并切换为hexo分支

   ```bash
   $ git clone https://github.com/chunyangzhao/chunyangzhao.github.io
   $ git checkout -b hexo origin/hexo
   ```

4. 删除chunyangzhao.github.io版本库中除了.git夹外的所有文件，将.git文件夹放到本地hexo目录中

5. 在hexo目录中，theme目录下的各个主题文件夹内可能包含有.git文件，由于git不支持嵌套，因此需要将主题文件夹内的.git文件删除后才能把主题文件夹push到github上去

6. 将hexo目录下的所有文件都添加到git中(包括已经删除的文件记录)，然后push到远端hexo分支

   ```bash
   $ git add -A
   $ git commit -m " "
   $ git push origin hexo
   ```

**上传到github过**

```bash
$ hexo clean
$ git status
$ git add [.md]
$ git commit -m ""
$ git push origin hexo
```

hexo clean后，目录内发生改变的只有你修改的博客文件，将其提交就好

### 将hexo目录从github更新到本地

**未下载hexo目录**

1. 先下载hexo部署文件，进入chunyangzhao目录

   ```bash
   $ git clone https://github.com/chunyangzhao/chunyangzhao.github.io
   ```

2. master分支是博客静态文件，hexo分支是hexo博客源文件，切换到hexo分支

   ```bash
   $ git checkout -b hexo origin/hexo
   ```

3. 安装hexo

   此时输入hexo -v 失败，提示ERROR Try running: 'rm -rf node_modules && npm install --force'

   ```bash
   $ rm -rf node_modules && npm install --force
   ```

   此时在执行hexo -v成功

4. 之后可进行正常hexo操作，编写、部署博客

**已下载hexo目录**

先切换到hexo分支，然后

```bash
$ git pull
```