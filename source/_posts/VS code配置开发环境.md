---
title: VScode配置C++/Java开发环境
copyright: true
abbrlink: 41bba354
notshow: false
tags:
  - C/C++
  - Java
categories: 学习
description: VScode配置C++/Java开发环境
image: 
- "https://data.singlelovely.cn/CoverPicture/41bba354.jpg!CoverPicture"
photos:
sticky:
date: 2019-03-08 23:56:00
password:
---

{% meting "548651034" "netease" "song" %}

## Java配置

```json launch.json
{
        "version": "0.2.0",
        "configurations": [
            {
                "type": "java",
                "name": "java",
                "request": "launch",
                "mainClass": "${file}",
                "console": "integratedTerminal", //使用vscode终端
                //"console": "externalTerminal"
            },
        ],
        "compounds": []
    }
```

可以将配置放在用户设置中，实先全局调用，如下：

```json settings.json
"launch": {
        "version": "0.2.0",
        "configurations": [
            {
                "type": "java",
                "name": "java",
                "request": "launch",
                "mainClass": "${file}",
                "console": "integratedTerminal",
                //"console": "externalTerminal"
            },
        ],
        "compounds": []
    }
```

### 插件

推荐安装 <span id="font-purple">Java Extension Pack</span> ，一共5个插件，一次安装到处使用

<span id="font-blue">Code Runner</span> ：安装完成后会在右上角出现一个运行按钮，支持多种语言的直接运行，不需要配置文件，缺点是不能调试。

如果只需要简单的运行调试功能，安装以下两个插件就好

<span id="font-blue">Debugger for Java</span>
<span id="font-blue">Language support for Java（TM）by Red Hat</span>

## C++配置

#### 准备条件

<p id = "div-border-top-purple">电脑上安装g++、gcc、gdb等编译调试环境，并配置环境变量</p>

因为<span id="inline-blue">launch.json</span>需要调用<span id="inline-blue">tasks.json</span>进行预编译，所以无法将配置写入setting.json中实现全局配置，需要在工作空间中配置.vscode目录

```json launch.json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "C/C++",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "F:/CMinGW/bin/gdb.exe",
            "preLaunchTask": "g++",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}

```

```json tasks.json
{
    "version": "2.0.0",
    "command": "g++",
    "args": ["-g","${file}","-o","${fileDirname}/${fileBasenameNoExtension}.exe"],
    "problemMatcher": {
        "owner": "cpp",
        "fileLocation": ["relative", "${workspaceRoot}"],
        "pattern": {
            "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",
            "file": 1,
            "line": 2,
            "column": 3,
            "severity": 4,
            "message": 5
        }
    }
}
```

### 插件

<span id="font-blue">C/C++</span> ：提供语言支持，debugging等功能。

<span id="font-blue">C++ Intellisense</span> ： 提供智能分析提示等。

## launch.json 文件属性值详解（java举例）

### Launch

- mainClass (required)： java 代码的 main 类 (例如：[mymodule/]com.xyz.MainClass).
- args： 传递给程序的命令行参数
- sourcePaths： 程序的额外源目录。默认情况下，调试器从项目设置中查找源代码。这个选项允许调试器在额外的目录中查找源代码
- modulePaths： 用于启动JVM的模块路径。如果没有指定，调试器将自动从当前项目解析
- classPaths： 启动JVM的类路径。如果没有指定，调试器将自动从当前项目解析
- encoding： 该文件中的JVM的编码设置。如果没有指定，将使用’UTF-8’。在 Supported Encodings 中可以找到可能的值
- vmArgs： JVM的额外选项和系统属性(例如：-Xms<size> -Xmx<size> -D<name>=<value>)
- projectName： 调试器在其中搜索类的首选项目。在不同的项目中可能会有重复的类名。当调试器在启动程序时查找指定的主类时，这个设置也可以工作。表达式求值是必须的
- cwd： 程序的工作目录
- env： 程序的额外环境变量
- stopOnEntry： 启动后自动暂停程序
- console： 用于启动程序的指定控制台。默认为 internalConsole 
- internalConsole： VS Code Debug 控制台 (输入不被支持)
- integratedTerminal： VS Code 集成终端
- externalTerminal： 可以在用户设置中配置的外部终端
- stepFilters： 在执行debug调试时，跳过指定的类或方法 
- classNameFilters： 跳过指定的类。类名应该完全限定，支持通配符
- skipSynthetics： 跳过synthetic 方法
- skipStaticInitializers： 跳过静态初始化方法
- skipConstructors： 跳过构造方法

### Attach

- hostName (required)： 远程调试器的主机名或IP地址
- port (required)： 远程调试器的debug端口
- timeout： 重新连接之前的超时时间，以毫秒为单位(默认为30000ms)
- sourcePaths： 程序的额外源目录。默认情况下，调试器从项目设置中查找源代码。这个选项允许调试器在额外的目录中查找源代码
- projectName： 调试器在其中搜索类的首选项目。在不同的项目中可能会有重复的类名。当调试器在启动程序时查找指定的主类时，这个设置也可以工作
- stepFilters： 在 debug 调试时，跳过指定的类或方法 
- classNameFilters： 跳过指定的类。类名应该完全限定，支持通配符
- skipSynthetics： 跳过 synthetic 方法
- skipStaticInitializers： 跳过静态初始化方法
- skipConstructors： 跳过构造方法

### User Settings

- java.debug.logLevel： 发送到VS代码的调试器日志的最低级别，默认为警告
- java.debug.settings.showHex： 在变量视图中以十六进制格式显示数字，默认为false
- java.debug.settings.showStaticVariables： 在variables视图中显示静态变量，默认为true
- java.debug.settings.showQualifiedNames： 在变量视图中显示完全限定的类名，默认为false
- java.debug.settings.maxStringLength： 变量视图或调试控制台中显示的最大字符串长度。超过此长度的字符串将被裁剪。默认值为0，表示没有进行修剪
- java.debug.settings.enableHotCodeReplace： 启用Java源代码的热代码替换。确保VScode 中的 Java 代码没有禁用自动构建。有关用法和限制的更多信息，请参阅 wiki page

## 后记

<p id = "div-border-left-green">为了不违背轻量化的本质，只实现单文件执行，及简单的项目运行。复杂项目还是用IDE。如果啥IDE干的事儿啥都能干，和直接装一个IDE又有何区别？？？</p>

## 参考内容

[Launch.json attributes](https://code.visualstudio.com/docs/editor/debugging#_launchjson-attributes)
[Writing Java with Visual Studio Code](https://code.visualstudio.com/docs/java/java-tutorial)
[Variables Reference](https://code.visualstudio.com/docs/editor/variables-reference)
[快速使用 vscode 进行 Java 编程](https://juejin.im/post/5ac193cd6fb9a028d208161c)
