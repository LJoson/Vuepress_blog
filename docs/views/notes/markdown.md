---
title: markown使用文档
date: 2021-05-02 15:05:12
sidebar: true
sidebarDepth: 5
tags: 
- 文档笔记
categories:
- "笔记类"
isShowComments: true
---



- markdown 插入视频
```
<iframe height=498 width=510 src="视频地址">
```

```
<iframe height=498 width=510 src="视频地址" frameborder=0 allowfullscreen></iframe>
```
2.markdown 插入gif
```
<iframe height=500 width=500 src="gif地址">
```

tree 命令部分常用命令

tree -a 显示所有
tree -d 只显示文档夹
tree -L n 显示项目的层级，n表示层级数，比如想要显示项目三层结构，可以用tree -l 3；
tree -I pattern 用于过滤不想要显示的文档或者文档夹。比如你想要过滤项目中的 node_modules 文档夹，可以使用
tree -I “node_modules”；
tree > tree.md 将项目结构输出到 tree.md 这个文档