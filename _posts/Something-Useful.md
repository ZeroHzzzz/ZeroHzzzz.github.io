---
title: Something Useful
date: 2024-02-21 15:16:33
categories:
sticky: 1
---

# 放一些有用的链接

[变量取名](https://unbug.github.io/codelf/)

[DeeL翻译](https://www.deepl.com/zh/translator)

[markdown查询](http://latex.codecogs.com/eqneditor/editor.php)

[md公式整理](https://muzing.top/posts/48740/)

[图论工具](https://csacademy.com/app/graph_editor/)

[脚本](https://greasyfork.org/zh-CN)

[壁纸](https://wallhaven.cc/)

[Flathub](https://flathub.org)

[Zeemo 自动加字幕/翻译字幕](http://zeemo.ai)

# 一些常用命令

## conda
```bash
conda env list
conda info --envs
conda create -n env_name python=...
conda activate env_name
conda deactivate
conda remove --name env_name --all  // 删除指定虚拟环境及其中所安装的包
conda remove --name env_name  package_name
conda env export --name myenv > myenv.yml
conda env create -f  myenv.yml
conda list pkgname*  //*号用于模糊查找
conda install package_name
conda uninstall package_name
```