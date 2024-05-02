---
title: 基于hexo搭建博客（GitHub）
date: 2023-10-27 10:58:06
categories: 
  - Technologies_exploration
  - Hexo
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
![Hello, World!](1.png)

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
# Addition
## 使用Fluid主题的一些文章属性设置
```title
---
title: Hexo Fluid主题使用笔记

tags:
  - Hexo
  [Hexo, Fluid]  # 推荐使用这种方法

categories:
  - Hexo
  - Fluid # 注意以上这两个标题不是并列关系，而是包含关系
  - Hexo
    - Fluid  # 注意以上这两个标题是并列关系
  - [Hexo, Fluid]  # 并列关系

excerpt: 这是摘要 # 摘要还可以在正文通过 <!-- more --> 进行分割

hide: true # 隐藏文章，隐藏后依然可以通过文章链接访问

sticky: 100 # 数值越大排序越靠前

index_img: /img/example.jpg # 文章在首页的封面图，支持外链

banner_img: /img/post_banner.jpg # 文章详情页顶部大图，支持外链

toc: true # 生成文章目录，不填为true
---

```
## 一些有意思的东西
```hexo
// 便签

{% note success %}
文字 或者 `markdown` 均可
{% endnote %}
或者使用 HTML 形式：
<p class="note note-primary">标签</p>


//行内标签

{% label primary @text %}
或者
<span class="label label-primary">Label</span>


//复选框

{% cb text, checked?, incline? %}

text：显示的文字
checked：默认是否已勾选，默认 false
incline: 是否内联（可以理解为后面的文字是否换行），默认 false


//按钮

{% btn url, text, title %}

或者：

<a class="btn" href="url" title="title">text</a>

url：跳转链接
text：显示的文字
title：鼠标悬停时显示的文字（可选）
```

# EOF