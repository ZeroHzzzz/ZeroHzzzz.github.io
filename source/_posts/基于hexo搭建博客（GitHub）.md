---
title: 基于hexo搭建博客（GitHub）
date: 2023-10-27 10:58:06
tags: Hexo
---

# 准备工作
- GitHub账号
- 安装git
- 安装node

# 创建仓库
- 创建仓库，并将仓库命名为 username.github.io
注意这里的username（）

# 安装hexo
- 安装hexo
```npm install -g hexo-cli```
- check
```hexo -v```
- 创建hexo项目并初始化
```
hexo init [hexo-blog(你新建的本地博客文件夹的名字，如果不输入默认为当前文件夹)]
cd hexo-blog
npm install
```
# 主题
hexo默认主题为landscape，可以前往hexo官网寻找你心仪的主题
[Themes](https://hexo.io/themes/)

```
git clone [github地址] [存放路径]
# 例如
# git clone https://github.com/iissnan/hexo-theme-next themes/next
```

在根目录的 _config.yml 文件中找到theme字段并将它改成你主题的名字
```theme: next```

本地启动：
```
hexo g
hexo s
```
{% asset_img 1.png 这里曾经有一张图片..... %}

# 修改参数
根据themes提供的文档修改参数

# Writing
新建文章
```hexo new post 测试文章```
然后就开始写吧

# 本地预览
- 预览的同时可以修改文章内容或主题代码，保存后刷新页面即可
- 对 Hexo 根目录 _config.yml 的修改，需要重启本地服务器后才能预览效果
```hexo s```

# Deloy
- 安装hexo-deployer-git
```npm install hexo-deployer-git --save```
- 修改根目录下的 _config.yml，配置 GitHub 相关信息,token获取方式自行百度
```
deploy:
  type: git
  repo: https://github.com/yaorongke/yaorongke.github.io.git
  branch: main
  token: ghp_3KakcaPHerunNRyMerofcFd9pblU282FSbsY   # 应该可写可不写
```
- 发布
```
hexo g -d
```

# EOF