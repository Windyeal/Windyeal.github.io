# Windyeal's Blog


> *power by [HUXPRO](https://huangxuan.me)*


## 个人博客建站练手项目 | 顺带记录学习笔记


POSTS 示例

```
---
layout:     post
title:      "大标题"
subtitle:   "标题简介"
#subtitle:   "🎞  Slides:Service Worker 101, Working Offline and Instant Loading (GDG DevFest 2016 Beijing)"
iframe:     "//huangxuan.me/sw-101-gdgdf/"
navcolor:   "invert"
date:       2025-7-30
author:     "Windyeal"
header-style: text
header-img: "img/post-bg-dreamer.jpg"
header-mask: 0.4
catalog: true
published: false

tags:
    - 示例1
    - 示例2
---
```

**一些markdown语法对照速查**

|mermaid-mindmap|写法示例|说明|
|---|---|---|
|普通节点|节点内容|直接输入|
|层级|缩进两个空格，每多一层多缩进2格|表示节点层级|
|默认折叠|节点名 :::|初始状态折叠|
|颜色|节点名 :::green 或 ::: #hex|绿色或自定义颜色|
|图标|fa:fa-xxx 节点内容|支持FontAwesome图标|
|加粗斜体|**加粗** ; *斜体*|与Markdown一致|
|复合修饰|fa:fa-xxx 文本 :::color|图标+颜色|

|mermaid-graph|语法示例|说明|
|---|---|---|
|开始|graph TD|自上向下排列|
|节点方	|A[文本]	|方框|
|圆角方框	|A(文本)	|圆角|
|圆形结点	|A((文本))	|圆形|
|菱形条件	|A{条件判断}	|决策点|
|单向箭头	|A --> B	|单向连接|
|有文字箭头	|A --说明--> B	|箭头上有文字|
|虚线	|A -.-> B	|虚线箭头|
|双向箭头	|A <--> B	|双向连接|
|子图	|subgraph 名称 ... end	|模块/分组|
|注释	|%% 注释内容	|行注释|

|数学符号|LaTeX 语法|
|---|---|
|上标（幂/指数）|	x^2	|
|下标|	x_1	|
|组合上下标|	x_i^2	|
|根号|	\sqrt{x}	|
|n 次根|	\sqrt[n]{x}	|
|分数|	\frac{a}{b}	|
|向量（用粗体）|	\vec{a} 或 \mathbf{a}|
|Greek字母|	\alpha, \beta, \gamma	|
|求和|	\sum_{i=1}^{n}	|
|积分|	\int_a^b	|
|乘号|	\times	|
|点乘|	\cdot	|
|除号|	\div	|
|≈|	\approx	|
|≠|	\neq	|
|≤|	\leq	|
|≥|	\geq|	
|→|	\to	|
|←|	\leftarrow	|
|无穷|	\infty	|
|空集|	\emptyset	|
|部分导数|	\partial	|
|大括号|	\left\{ ... \right\}	|
|省略号|	\cdots 或 \ldots |
|括号自动加大|	\left( ... \right)|
|列向量|	\begin{bmatrix} a \\ b \end{bmatrix}	|
|行向量|	\begin{bmatrix} a & b \end{bmatrix}	|
|n 维单位向量|	\hat{\mathbf{e}}_i	|
|上标是括号内表达式|a^{b+c}|
|下标是复合 |a_{ij}	|
|带箭头的向量|\overrightarrow{AB}|
|加点（时间导数）|\dot{x}|	
|加上横线，常用于均值|\bar{x}	|
|加下划线 |\underline{x}|

Other Resources
---------------

Ports
- [**Hexo**](https://github.com/Kaijun/hexo-theme-huxblog) by @kaijun
- [**React-SSR**](https://github.com/LucasIcarus/huxpro.github.io/tree/ssr) by @LucasIcarus

[Starter/Boilerplate](https://github.com/huxpro/huxblog-boilerplate)
- Out of date. Helps wanted for updating it on par with the main repo

Translation
- [🇨🇳  中文文档（有点过时）](https://github.com/Huxpro/huxpro.github.io/blob/master/_doc/README.zh.md)


License
-------

Apache License 2.0.
Copyright (c) 2015-present Huxpro

Hux Blog is derived from [Clean Blog Jekyll Theme (MIT License)](https://github.com/BlackrockDigital/startbootstrap-clean-blog-jekyll/)
Copyright (c) 2013-2016 Blackrock Digital LLC.
