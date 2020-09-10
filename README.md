# test_vscode_c-
# Test-vscode-cplus

### 项目介绍
测试VS code编写c++程序，并使用git管理

### vscode环境配置过程
1. 安装 `C/C++` 插件
2. 按`Ctrl+Shift+p`，输入`C/CPP`，编辑设置，配置`c_cpp_properties.json`
```
c_cpp_properties.json
    {
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**",
                "E:/Windows Kits/10/Include/10.0.17134.0/cppwinrt/winrt",
                "E:/Windows Kits/10/Include/10.0.17134.0/shared",
                "E:/Windows Kits/10/Include/10.0.17134.0/ucrt",
                "E:/Windows Kits/10/Include/10.0.17134.0/um",
                "E:/Windows Kits/10/Include/10.0.17134.0/winrt",
                "E:/Program Files/Microsoft/VisualStudio/VC/Tools/MSVC/14.14.26428/include/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "intelliSenseMode": "msvc-x64"
        }
    ],
    "version": 4
}
```
4. 按`Ctrl+Shift+p`，输入`Tasks`,点击`配置任务`，配置`Tasks.json`
```
Tasks.json
    {
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "build",
            "type": "shell",
            "command": "cl",
            "args": [
                "*.cpp",
                ]
        },
        {
            "label": "run",
            "type": "shell",
            "command": "",
            "args": [
                ".\\add.exe",
                ]
        }
    ]
}
```

### 环境配置问题
 1. ‘cl’ 不是内部或外部命令，也不是可运行程序或批处理文件
 
    上述错误表示系统找不到 cl.exe 这个文件。此文件位于 C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.11.25503\bin\HostX64\x64 中（再次提醒，不同操作系统或不同 VS 版本，所示路径可能会有所不同）。

      解决方法为，右键此电脑，选择“属性”，“高级系统设置”，“环境变量”。在下方的“系统变量”中找到变量 path，选择“编辑”，“新建”。将上述路径添加进此变量即可。



2. “fatal error C1034: iostream: 不包括路径集”或“fatal error C1083: 无法打开包括文件: “corecrt.h”: No such file or directory”

    上述错误表示系统找不到 iostream 或者 corecrt.h 这个文件。C++ 的头文件们分别保存在下述目录中。

      解决方法为，右键此电脑，选择“属性”，“高级系统设置”，“环境变量”。在下方的“系统变量”中选择变量 INCLUDE，若没有此变量，则选择“新建”，变量名为“INCLUDE”，变量值列在下方：
```
      C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.11.25503\include

      C:\Program Files (x86)\Windows Kits\10\Include\10.0.15063.0\shared

      C:\Program Files (x86)\Windows Kits\10\Include\10.0.15063.0\ucrt

      C:\Program Files (x86)\Windows Kits\10\Include\10.0.15063.0\um

      C:\Program Files (x86)\Windows Kits\10\Include\10.0.15063.0\winrt

      注意：路径之间用英文分号隔开。
```


3. fatal error LNK1104: 无法打开文件“libcpmt.lib”

    上述问题表示系统找不到 .lib 文件。这些文件的路径列在下方。

      解决方法为，右键此电脑，选择“属性”，“高级系统设置”，“环境变量”。在下方的“系统变量”中选择变量 LIB，若没有此变量，则选择“新建”，变量名为“LIB”，变量值列在下方：
```
      C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.11.25503\lib\x64

      C:\Program Files (x86)\Windows Kits\10\Lib\10.0.15063.0\ucrt\x64

      C:\Program Files (x86)\Windows Kits\10\Lib\10.0.15063.0\um\x64

     注意：路径之间用英文分号隔开。
```

  如果上述三个步骤全部完成，还是出现问题，可能的情况及解决办法有：

  1. 检查上述所有路径全部保存在了正确的变量名底下；

  2. 重启 cmd 窗口并重新尝试；

  3. 系统为 32/64 位却添加了另一方的路径



### git使用说明

1. git init
2. git remote add "remote name" url
3. git pull <远程主机名> <远程分支名>:<本地分支名> 将连个不相关的项目合并到本地
4. 3 添加参数'--allow-unrelated-histories' 解决refusing to merge unrelated histories问题
5. git push <远程主机名> <本地分支名>:<远程分支名> 将合并的项目上传到远程主机
[参考这里](http://www.runoob.com/manual/git-guide/)

### makefile编写说明
[参考这里](https://blog.csdn.net/gameboy12615/article/details/5778040)
