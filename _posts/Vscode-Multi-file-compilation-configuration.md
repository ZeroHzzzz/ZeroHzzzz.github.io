---
title: Vscode 多文件编译配置
date: 2023-12-02 13:34:04
categories:
    - Technologies_exploration
    - VSCode
---
## 正片开始
默认VSCode 只能编译单个文件，若多个文件一起编译，经常会报 undefined reference 找不到引用的错误，比如下面的问题：

```
"C:\Program Files\mingw64\bin\g++.exe" -fdiagnostics-color=always -g C:\Users\ZeroHzzzz\Desktop\dd\dd.cpp -o C:\Users\ZeroHzzzz\Desktop\dd\dd.exe
C:\Users\ZEROHZ~1\AppData\Local\Temp\ccYQ5ExK.o: In function `main':
C:/Users/ZeroHzzzz/Desktop/dd/dd.cpp:6: undefined reference to `maxn(int, int)'
collect2.exe: error: ld returned 1 exit status 
```

解决方法如下：
- 配置一下`.vscode `文件夹下的 `tasks.json` 就好了。
- tasks.json的话，就把界面点到代码的界面，然后菜单栏`"Terminal"` - `"Configure Tasks..."` 生成默认的`tasks.json`

找到 tasks.json中的 args 选项，这个主要是用来配置待编译的文件信息的，`${file} `替换成 ` ${workspaceFolder} `, 结果如下：

```json
"args": [
    "-fdiagnostics-color=always",
    "-g",
    "${workspaceFolder}\\*.cpp",
    "-o",
    "${fileDirname}\\${fileBasenameNoExtension}.exe"
],
```

再次运行程序，就可以多文件正常编译了

## Addition

但是如果我们还有其它的二级目录，那就还需要修改`tasks.json`文件。

【举例】main函数所在`test.cpp`在一级目录下，其它`cpp`文件在 `others `目录下，这个时候就需要把`tasks.json`改成：

```json
"args": [
    "-fdiagnostics-color=always",
    "-g",
    "${workspaceFolder}\\*.cpp",
    "${workspaceFolder}\\others\\*.cpp", //修改项
    "-o",
    "${fileDirname}\\${fileBasenameNoExtension}.exe"
],
```