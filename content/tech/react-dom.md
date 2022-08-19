---
title: react-dom
tags: 
- React
date: 2019-06-17 20:50:50
permalink:
categories:
- React
description:
image:
---
<p class="description"></p>

<img src="https://" alt="" style="width:100%" />

<!-- more -->

## 初识React

### react-dom 渲染过程
#### one
```markdown
state 数据 
JSX 模板
数据 + 模板结合，生成真实的DOM, 来显示
state数据发生改变
数据 + 模板结合，生成真实的DOM,替换原始的DOM
```
#### 缺陷 
第一次生成了一个完整的DOM片段
第二次生成了一个完整的DOM片段
第二次的DOM替换第一次的DOM,非常耗性能
#### two
```markdown
state 数据 
JSX 模板
数据 + 模板结合，生成真实的DOM, 来显示
state数据发生改变
数据 + 模板结合，生成真实的DOM,并不直接替换原始的DOM
新的DOM和原始的DOM做比对，找差异
用新的DOM（DoucumentFragment）元素替换老的DOM元素
```
#### 缺陷
性能的提升并不明显

#### three
```markdown
state 数据 
JSX 模板
数据 + 模板结合 生成虚拟DOM（虚拟DOM就是一个JS对象, 用它来描述真实的DOM）
用虚拟DOM的结构生成真实的DOM, 来显示 
state数据发生改变
数据 + 模板结合， 生成新虚拟DOM（极大的提升了性能）
比较原始虚拟DOM和新的虚拟DOM的区别，找出区别中的内容
直接操作DOM,改变元素中的内容
``` 
#### 优点
性能提升了
它使得跨端应用得以实现,React Native
<hr />