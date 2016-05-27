---
title: '[译] IntelliJ IDEA 快捷键操作'
date: 2016-05-17 16:02:15
tags: [Java,JetBrains]
categories: [Translation]
---


捷克公司 JetBrains 推出的一系列 IDE 用着都很顺手，尤其是针对 Java 开发的 IDEA。不多说，欲善其事，先利其器。IDEA 有着相当完善的键盘操作，为了避免时不时去翻看手册，索性把官方的默认 Keymap 翻译成中文。

<!-- more -->

## 编辑

Ctrl + Space: 基本代码补全（类、方法或变量名）
Ctrl + Shift + Space: 智能代码补全（根据类型过滤待选的方法和变量列表）
Ctrl + Shift + Enter: 补全语句
Ctrl + P: 参数信息（在方法内调用参数）
Ctrl + Q: 快速查看文档
Shift + F1: 外部文档
Ctrl + F1: 显示光标所在处的错误或警告信息
Alt + Insert: 生成代码（Getters, Setters, Constructors, hashCode/equals, toString）
Ctrl + O: 重写父类方法
Ctrl + I: 实现接口方法
Ctrl + Alt + T: 包裹代码（if..else, try..catch, for, synchronized, etc.）
Ctrl + /: 注释/取消注释当前行
Ctrl + Shift + /: 注释/取消注释代码块
Ctrl + W: 层次递增地选中代码块
Ctrl + Shift + W: 对当前选中的代码块层次递减的回到之前的选中状态（Ctrl + W 的逆过程）
Alt + Q: 上下文信息
Alt + Enter: 显示意图动作和快速修复
Ctrl + Alt + L: 格式化代码
Ctrl + Alt + O: 优化 imports
Ctrl + Alt + I: 自动缩进行
Tab / Shift + Tab: 缩进/回退当前选中的行
Ctrl + X or Shift + Delete: 剪切当前行或选中的代码块到剪贴板
Ctrl + C or Ctrl + Insert: 复制当前行或选中的代码块到剪贴板
Ctrl + V or Shift + Insert: 从剪贴板黏贴
Ctrl + Shift + V: 从当前 buffers 中黏贴
Ctrl + D: 复制当前行或选中的代码段到后一位置
Ctrl + Y: 删除光标所在行
Ctrl + Shift + J: 智能行拼接
Ctrl + Enter: 智能行分拆
Shift + Enter: 新增一行
Ctrl + Shift + U: 变更光标所在单词或选中代码段的大小写
Ctrl + Shift + ] / [: 向上/向下选中代码直到代码块的结束/开始位置
Ctrl + Delete: 向后删除到单词尾
Ctrl + Backspace: 向前删除到单词头 
Ctrl + NumPad+/-: 展开/并拢代码块
Ctrl + Shift + NumPad+: 展开全部代码
Ctrl + Shift + NumPad-: 收拢全部代码
Ctrl + F4: 关闭当前 tab
Alt + Shift + Inert: 开启/关闭列选择模式

## 查找/替换

Double Shift: 全局查找文件
Ctrl + F: 当前文件内查找
F3: 查找下一个
Shift + F3: 查找上一个	
Ctrl + R: 替换
Ctrl + Shift + F: 指定路径内查找	
Ctrl + Shift + R: 制定路径内替换
Ctrl + Shift + S: 按结构搜索
Ctrl + Shift + M: 按结构替换

## 使用搜索

Alt + F7 / Ctrl + F7: 查找当前文件内的使用情况
Ctrl + Shift + F7: 高亮当前文件内的使用情况
Ctrl + Alt + F7: 显示使用情况

## 编译及运行

Ctrl + F9: Make project
Ctrl + Shift + F9: 编译选中的文件，包或模块
Alt + Shift + F10: 选择配置并运行
Alt + Shift + F9: 选择配置并调试
Shift + F10: 运行
Shift + F9: 调试
Ctrl + Shift + F10: 运行当前编辑的上下文配置	

## 调试

F8: 单步执行（不对子函数进行单步执行）
F7: 单步执行（对子函数继续单步执行）
Shift + F7: 智能单步执行（对子函数继续单步执行）
Shift + F8: 单步执行进子函数内部时，跳出子函数
Alt + F9: 运行到鼠标位置
Alt + F8: 计算变量值
F9: 继续执行程序
Ctrl + F8: 创建/取消断点
Ctrl + Shift + F8: 浏览断点

## 导航

Ctrl + N: 跳转到 class
Ctrl + Shift + N: 跳转到文件
Ctrl + Alt + Shift + N: 跳转到变量
Alt + Right/Left: 跳转到后/前一个编辑 tab
F12: 跳转到上一个工具窗口
Esc: 跳转到编辑器（从工具窗口）
Shift + Esc: 隐藏活动窗口或最近一个活动窗口
Ctrl + Shift + F4: 关闭活动的 run/messages/find/... 标签
Ctrl + G: 跳转到指定行
Ctrl + E: 打开最近文件列表
Ctrl + Alt + Left/Right: 跳转至前一次/后一次浏览的位置
Ctrl + Shift + Backspace: 跳转到上一次编辑的位置
Alt + F1: 在任意视图中选择当前文件或符号
Ctrl + B or Ctrl + Click: 跳转至声明
Ctrl + Alt + B: 跳转至实现
Ctrl + Shift + I: 快速查阅定义
Ctrl + Shift + B: 跳转至类型声明
Ctrl + U: 跳转至父类的方法/父类的类
Alt + Up/Down: 跳转到前一个/后一个方法
Ctrl + ] / [: 跳转到代码块的结束/开始位置
Ctrl + F12: 弹出类结构视图
Ctrl + H: 显示类继承关系
Ctrl + Shift + H: 显示方法继承关系
Ctrl + Alt + H: 显示调用关系
F2 / Shift + F2: 下一个/前一个高亮的错误
F4 / Ctrl + Enter: 编辑/浏览源码
Alt + Home: 显示导航栏
F11: 设置/取消书签
Ctrl + F11: 设置/取消书签（带助记符）
Ctrl + #[0-9]: 跳转到指定书签
Shift + F11: 显示全部书签

## 重构

F5: 复制
F6: 移动
Alt + Delete: 安全删除
Shift + F6: 重命名 
Ctrl + F6: 更改签名
Ctrl + Alt + N: 内联
Ctrl + Alt + M: 抽取方法
Ctrl + Alt + V: 抽取变量
Ctrl + Alt + F: 抽取域
Ctrl + Alt + C: 抽取常量
Ctrl + Alt + P: 抽取参数 

## 版本控制/本地历史

Ctrl + K: 提交到 VCS
Ctrl + T: 从 VCS 更新工程
Alt + Shift + C: 查看最近改动
Alt + BackQuote (`): VCS 快速浏览

## 动态模板

Ctrl + Alt + J: 用动态模板包裹
Ctrl + J: 插入动态模板

## 通用

Alt + #[0-9]: 打开对应的工具窗口
Ctrl + S: 保存全部文件
Ctrl + Alt + Y: 同步工程
Ctrl + Shift + F12: 最大化/常规化编辑器窗口
Alt + Shift + F: 添加到 Favorites
Alt + Shift + I: 根据配置检查当前文件
Ctrl + BackQuote (`): 快速切换当前 scheme
Ctrl + Alt + S: 打开设置对话框
Ctrl + Alt + Shift + S: 打开项目结构对话框
Ctrl + Shift + A: 查找动作指令
Ctrl + Tab: 在编辑标签和工具窗口之间切换