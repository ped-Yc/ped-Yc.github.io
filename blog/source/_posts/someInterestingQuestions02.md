---
title: 【一些有趣的问题】01，事件循环
date: 2021-02-23 10:15:54
tags: [JS]
categories: [一些有趣的问题]
---

`以下语句会如何输出？`
```javascript
console.log('start')

setTimeout(() => {
  console.log('setTimeout')
}, 0)

new Promise((resolve) => {
  console.log('promise')
  resolve()
})
  .then(() => {
    console.log('then1')
  })
  .then(() => {
    console.log('then2')
  })

console.log('end')
```

结果：打印 start promise end then1 then2 setTimeout

原因：简单来说，JS代码的执行顺序为：同步代码-->异步代码（微任务-->宏任务）

分析：

1. 打印start

2. setTimeout 加入消息队列

3. new Promise 的同步部分执行，打印promise，then 部分加入消息队列

4. 打印end

5. 消息队列中先处理微任务 then 的部分，打印then1，then2

6. 消息队列处理宏任务 setTimeout，打印setTimeout

## `参考资料`
> [并发模型与事件循环](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/EventLoop)
>
> [深入理解js事件循环机制（浏览器篇）](http://lynnelv.github.io/js-event-loop-browser)