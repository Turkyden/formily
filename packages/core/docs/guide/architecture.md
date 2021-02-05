# 核心架构

## 领域模型

Formily 内核架构非常复杂，因为要解决一个领域级的问题，而不是单点具体的问题，先上架构图：

![](https://img.alicdn.com/imgextra/i1/O1CN01G1wPoK22TT2jDwSmh_!!6000000007121-2-tps-2854-2422.png)

## 说明

从上图中我们可以看到 Formily 内核其实是一个 Mobx 领域模型，整个领域模型核心是以下几个模型：

- Form 模型
  - Form 模型负责维护全局型的表单数据，同时负责管理表单下的所有字段集
- Field 模型
  - ArrayField/ObjectField 继承自 Field 模型，只是增加了自身特色的 Setters
  - Field 模型主要维护单个字段的状态，同时还会往 Form 模型里冒泡消息
- VoidField 模型
  - 作为一个虚字段模型，它不能控制表单值，只能控制它自己或子级字段的显示隐藏，交互模式等
- 节点树模型
  - 所有的字段都在一个集合上，集合的 key 是字段的节点路径，描述了节点与节点的父子层级关系，通过这个路径可以做到字段间的数据状态链接

实际消费领域模型则主要是依赖 Mobx 的 autorun 机制做依赖追踪来消费