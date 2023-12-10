---
title: Hexo添加图片的几种方式
date: 2023-10-27 10:36:10
categories:
    - Technologies_exploration
    - Hexo
---

在写文章的时候我们常常会使用图片来传达一些只可意会不可言传的含义....

# 绝对路径

当Hexo项目中只用到少量图片时，可以将图片统一放在source/images文件夹中，通过markdown语法访问它们。
路径：source/images/image.jpg
```![](/images/image.jpg)```


这样图片既可以在首页内容中访问到，也可以在文章正文中访问到。

# 相对路径

图片除了可以放在统一的images文件夹中，还可以放在文章自己的目录中。文章的目录可以通过配置_config.yml来生成。

在根目录的_config.yml中：

```post_asset_folder: true```
但是据我惨痛的经历显示，下面这种写法是错误的:
```![photo](passage_name/Photo.png)```
因此我翻阅了hexo的[文档](https://hexo.io/zh-cn/docs/)，里面是这么写的



{% asset_img 1.png 这里曾经有一张图片..... %}



但是不知道为啥这个艾斯比东西就是没有用....

因此我还是只能采用官方推荐的这种写法：
```{% asset_img example.jpg failed_description %}```

事后经过一翻谷歌搜索发现用md直接导入图片导致失败的原因可能是因为只是将图片放入文件夹，hexo生成静态界面时并没有处理该图片，所以运行后就找不到图片了....
给我整无语了。但是我发现他文件路径是这样的:
```https://zerohzzzz.github.io/[passage_name]/1.png```
而用`{% %}`方式导入图片，图片的路径是这样的：
```https://zerohzzzz.github.io/2023/10/27/[passage_name]/1.png```

~~这个艾斯比东西果然*****~~

但是这个问题似乎在插件的新版本中得到了解决，有兴趣可以看看[hexo-easy-images](https://github.com/boboidream/hexo-easy-images)，但我认为有`{% %}`方式就已经足够了


# Addition

[hexo+typora的图片路径问题](http://codecook.site/2020/12/05/hexo+typora%E7%9A%84%E5%9B%BE%E7%89%87%E8%B7%AF%E5%BE%84%E9%97%AE%E9%A2%98/)