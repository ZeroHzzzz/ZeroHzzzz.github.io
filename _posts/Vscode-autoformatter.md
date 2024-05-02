---
title: Vscode 自动格式化插件
date: 2024-03-17 04:16:37
categories:
    - Technologies_exploration
    - VSCode
---

# Previous

事情的起因是我在某一天打开 vscode 后发现了 tab 变成了两个空格而导致我这个极度代码洁癖的人感觉很难受
~~由于懒~~...由于习惯了编写 go 语言代码保存时候的自动格式化，这让最近因为 c++的~~goushi~~作业而焦头烂额的我开始思考能不能在其他语言编写的时候能不能也搞个

由于我平时使用的是 Vscode，因此我就直接使用了 prettier 插件。以下是我配置的一些记录：

# 步骤

-   安装 prettier 插件
-   配置
    -   可以通过 setting.json 进行配置， 这里就不多说了
    -   也可以通过在 setting 中直接搜索 prettier 来实现

```json
"editor.formatOnSave": true,  // 保存自动格式化
"prettier.useTabs": true,
"prettier.tabWidth": 4, // Tab 宽度
"C_Cpp.clang_format_style": "{ BasedOnStyle: Chromium, IndentWidth: 4}" // c++/c 大括号不换行
```
