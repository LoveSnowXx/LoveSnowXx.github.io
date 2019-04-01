---
title: V16.3 React
date: 2019-04-01 09:06:34
tags: 前端 | React
---
### React V16.3

#### 新增生命周期函数：

- getDerivedStateFromProps
- getSnapshotBeforeUpdate

getDerivedStateFromProps替代componentWillReceiveProps。

Ajax请求放在componentDidMount更合适。因为componentWillMount可能会被调用多次。

#### deprecate周期函数

- componentWillReceiveProps
- componentWillMount
- componentWillUpdate

getDerivedStateFromProps取代componentWillReceiveProps是不准确的说法。因为componentWillReceiveProps只在Updating过程中才被调用，而且只在因为父组件引发的Updating过程中才被调用。**getDerivedStateFromProps在Updating和Mounting过程中都会被调用。**

#### 总结

用一个静态函数getDerivedStateFromProps来取代被deprecate的几个生命周期函数，就是强制开发者在render之前只做无副作用的操作，而且能做的操作局限在根据props和state决定新的state，而已。