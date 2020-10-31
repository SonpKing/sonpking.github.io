---
title: Hexo + Next + GitHub + Gitalk
comments: true
categories: 教程 
---
本文主要介绍Hexo + Next在GitHub上自动部署教程。

## 准备

### Hexo
> 一个轻量级的静态博客框架，方便灵活，深受程序员喜爱。

### Next
> Hexo的一款主题，简介美观。

### GitHub
> 世界上最大开源项目托管空间，本文借助GitHub托管[本博客](https://blog.hoobo.net)的源代码，利用GitHub Pages托管博客网页，使用GitHub Actions实现博客的自动部署。

### gitalk
> 一款评论系统插件，它是基于GitHub issue实现的。优点是免费，无限空间。缺点是，每一篇博客都需要作者登陆GitHub开启一个新的issue。

## 安装

### Github创建博客仓库
- 登陆GitHub，创建名为username.github.io的仓库。同时创建两个分支，第一个`source`，用于保存源代码，同时设为主分支；第二个分支名为`master`，用于托管博客网页。
- 找到Settings > github pages。选择branch为`master`。custom domain里填入自己的域名，例如‘blog.hoobo.net’。此时source分支里应该多了一个‘CNAME’文件。
![](/images/posts/hexo_next_githu_gitalk01.png)
- 点击Actions，创建一个新的文件pages.yml，并用下面的代码代替默认代码
```yml
name: Pages

on:
  push:
    branches:
      - source  # default branch

jobs:
  pages:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 12.x
        uses: actions/setup-node@v1
        with:
          node-version: '12.x'
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: master  # deploying branch
```
- clone仓库到本地名为Blog的文件夹

### 本地仓库下载和配置
- 安装node.js和git
- 参考[文档](https://hexo.io/zh-cn/docs/)安装hexo并初始化
- 将‘CNAME’文件移入source文件夹，为了可以使用自定义域名
- 使用npm安装next主题
```sh
cd hexo-site
npm install hexo-theme-next
```
- 修改next主题的配置文件。为了避免修改hexo-theme-next包，从`./node_modules/hexo-theme-next/_config.yml`拷贝到`./_config.next.yml`并参照本博客的[_config.next.yml](https://github.com/SonpKing/sonpking.github.io/blob/source/_config.next.yml)修改。
- 参照本博客的[_config.yml](https://github.com/SonpKing/sonpking.github.io/blob/source/_config.yml)修改hexo配置文件`./_config.yml`。
```yml
url: http://blog.hoobo.net
theme: next
```

### Gitalk评论系统配置
- 在GitHub上找到Settings Developer > settings > OAuth Apps > New OAuth App新建一个Application
- 找到新建Application的Client ID和Client secret，修改配置文件_config.next.yml
```yml
gitalk:
  enable: true
  github_id: SonpKing # GitHub repo owner
  repo: sonpking.github.io # Repository name to store issues
  client_id: xxxx # GitHub Application Client ID
  client_secret: xxxx # GitHub Application Client Secret
  admin_user: [SonpKing]
  distraction_free_mode: true # Facebook-like distraction free mode
```

### 推送本地分支到远程分支
- 运行命令，本地调试。浏览器打开localhost:4000，查看博客是够正常显示。
```sh
hexo s
```
- 将本地的source分支推送到远程的source分支，稍等1-3分钟，GitHub Actions将会自动部署。
![](/images/posts/hexo_next_githu_gitalk02.png)
- 浏览器输入自定义域名，例如`blog.hoobo.net`。确认博客部署成功。

### 更新博客
- 在‘_post’文件夹下创建新的md文件
- 参考`推送本地分支到远程分支`