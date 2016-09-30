---
title: sublime 使用记录
date: 2016-09-30 15:12:00
categories:
tags: [sublime]
keywords:
description: sublime 初探索
---

# <font color="#4590a3" size = "6px">快捷方式记录</font>
Ctrl + Enter 在当前行下面新增一行然后跳至该行
Ctrl + Shift + Enter 在当前行上面增加一行并跳至该行

Ctrl + Shift + ↑/↓ 移动当前行
Ctrl + Shift + ←/→ 进行逐词选择
Ctrl + ←/→ 进行逐词移动
Ctrl + ↑/↓ 移动当前显示区域


Ctrl + M 可以快速的在起始括号和结尾括号间切换
Ctrl + Shift + M 则可以快速选择括号间的内容
Ctrl + Shift + Space：快速选择当前作用域（Scope）的内容

Ctrl+K+K 从光标处开始删除代码至行尾

Ctrl + Shift + T恢复刚刚关闭的标签

Ctrl + Shift + L 可以将当前选中区域打散，然后进行同时编辑
Ctrl + J 可以把当前选中区域合并为一行

Ctrl + shift + D 复制选中内容，下行展示
Ctrl + X 剪切当前行内容
Ctrl + Z 回退操作

Ctrl+Shift+K 删除整行。
Ctrl+/ 注释单行。
Ctrl+Shift+/ 注释多行。
Ctrl+K+U 转换大写。

Ctrl + D选择当前光标所在的词并高亮该词所有出现的位置，再次Ctrl + D选择该词出现的下一个位置，在多重选词的过程中，使用Ctrl + K进行跳过，使用Ctrl + U进行回退，使用Esc退出多重编辑。

Ctrl + K + B显示或隐藏侧栏
Shift + F11：切换无干扰全屏

Alt + Shift + 2进行左右分屏，Alt + Shift + 8进行上下分屏，Alt + Shift + 5进行上下左右分屏（即分为四屏）。分屏之后，使用Ctrl + 数字键跳转到指定屏，使用Ctrl + Shift + 数字键将当前屏移动到指定屏。例如，Ctrl + 1会跳转到1屏，而Ctrl + Shift + 2会将当前屏移动到2屏。

# <font color="#4590a3" size = "6px">跳转（Jumping）</font>
**Ctrl + P 调出文件切换面板**
- 输入需要查找的文件关键字，enter 编辑该文件
- 输入 @ 或直调Ctrl + R，罗列出来了这个文件当中的所有的Function,Ctrl + R会列出当前文件中的符号（例如类名和函数名，但无法深入到变量名）
- 输入一个英文冒号 : 或 直调Ctrl + G然后再输入一个数字，则可以跳到指定的行数，Ctrl + G输入行号以跳转到指定行
- 输入一个 # 号，可以罗列/搜索文本
- ***Ctrl+P ，输入`setting@depend`车（模糊匹配）,j即可打开这个文件并定位到函数中***
**Ctrl+Shift+P 强大的命令面板**
- 输入`Swap Case`可以将选中的文本大小写反转
- `Save All`可以一次保存全部文件；
- `Close All`一次关闭全部文件

# <font color="#4590a3" size = "6px">查找&替换（Finding&Replacing）</font>
*快速查找&替换*

- 多数情况下，我们需要查找文中某个关键字出现的其它位置，这时并不需要重新将该关键字重新输入一遍然后搜索，我们只需要使用Shift + ←/→或Ctrl + D选中关键字，然后F3跳到其下一个出现位置，Shift + F3跳到其上一个出现位置，此外还可以用Alt + F3选中其出现的所有位置（之后可以进行多重编辑，也就是快速替换）。

* 标准查找&替换
- 搜索某个已知但不在当前显示区域的关键字，这时可以使用`Ctrl + F`调出搜索框进行搜索,以及使用Ctrl + H进行替换.

*关键字查找&替换*

- 对于普通用户来说，常规的关键字搜索就可以满足其需求：在搜索框输入关键字后Enter跳至关键字当前光标的下一个位置，Shift + Enter跳至上一个位置，Alt + Enter选中其出现的所有位置（同样的，接下来可以进行快速替换）。

- Sublime Text的查找有不同的模式：Alt + C切换大小写敏感（Case-sensitive）模式，Alt + W切换整字匹配（Whole matching）模式，除此之外Sublime Text还支持在选中范围内搜索（Search in selection），这个功能没有对应的快捷键，但可以通过以下配置项自动开启。"auto_find_in_selection": true 这样之后在选中文本的状态下范围内搜索就会自动开启，配合这个功能，局部重命名（Local Renaming）变的非常方便.使用Ctrl + H进行标准替换，输入替换内容后，使用Ctrl + Shift + H替换当前关键字，Ctrl + Alt + Enter替换所有匹配关键字。

*多文件搜索&替换*

- 使用Ctrl + Shift + F开启多文件搜索&替换（注意此快捷键和搜狗输入法的简繁切换快捷键有冲突）,多文件搜索&替换默认在当前打开的文件和文件夹进行搜索/替换，我们也可以指定文件/文件夹进行搜索/替换。

# 引用
引用链接[神级代码编辑器 Sublime Text 全程指南](http://www.cocoachina.com/programmer/20150715/12550.html)
引用链接[Sublime Text神级代码编辑器的一个介绍](http://blog.l1n3.net/editor/sublime-text-introduce/)
引用链接[Sublime Text非官方文档（中文翻译版）](http://sublime-text.readthedocs.io/en/latest/index.html)
引用链接[Sublime Text 3 配置和使用方法](https://www.zybuluo.com/king/note/47271)
