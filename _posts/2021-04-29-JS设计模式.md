---
title: JS设计模式
author: zq
date: 2022-04-29
category: contest
layout: post
---

![23种设计模式](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/4/6/169f16406d230ffe~tplv-t2oaga2asx-watermark.awebp)

### 创建型：

#### 构造器模式：

使用构造函数去初始化对象，抽象了每个对象实例的变与不变

#### 工厂模式：

**将创建对象的过程单独封装**，抽象不同构造函数（类）之间的变与不变

1. 简单工厂

2. 抽象工厂
   
   开放封闭原则：**软件实体（类、模块、函数）可以扩展，但是不可修改**
   
   - 抽象工厂：用于给工厂extends
   - 具体工厂：用于创建具体的类
   - 抽象类：用于给类extends
   - 具体类：用于创建实例

#### 单例模式：

**保证一个类仅有一个实例，并提供一个访问它的全局访问点**

实现单例的思路：

1. 闭包
   
   ```javascript
   const Modal = (function() {
           let modal = null
           return function() {
               if(!modal) {
                   modal = document.createElement('div')
                   modal.innerHTML = '我是一个全局唯一的Modal'
                   modal.id = 'modal'
                   modal.style.display = 'none'
                   document.body.appendChild(modal)
               }
               return modal
           }
       })()
   ```

2. 类的静态变量
   
   ```javascript
   class Storage {
       static getInstance() {
           // 判断是否已经new过1个实例
           if (!Storage.instance) {
               // 若这个唯一的实例不存在，那么先创建它
               Storage.instance = new Storage()
           }
           // 如果这个唯一的实例已经存在，则直接返回
           return Storage.instance
       }
       getItem (key) {
           return localStorage.getItem(key)
       }
       setItem (key, value) {
           return localStorage.setItem(key, value)
       }
   }
   ```

### 结构型

#### 原型模式：

在原型模式下，当我们想要创建一个对象时，会先找到一个对象作为原型，然后通过**克隆原型**的方式来创建出一个与原型一样（共享一套数据/方法）的对象。在 JavaScript 里，`Object.create`方法就是原型模式的天然实现

#### 装饰器模式：

- 将本身逻辑单独封装，实现新功能时不关心现有业务逻辑如何，只关心新功能如何实现

- 单一职责原则

- ES7 中的装饰器
  
  1. 装饰器直接放入浏览器/Node中运行会报错需要安装Babel转码

#### 适配器模式：AJAX请求适配

#### 代理模式：

- > 一个对象**不能直接访问**另外一个对象，需要一个**代理**而间接达到访问目的，这样的模式是代理模式

- 最常见四种：
  
  - 事件代理（事件冒泡）
  - 虚拟代理（图片预加载）
  - 缓存代理
  - 保护代理（Proxy）

### 行为型

#### 策略模式：

- 单一功能：一个函数只有一个明确的分工，易于逻辑定位
- 开放封闭：对扩展开放，对修改封闭----对象映射

> 定义一系列的逻辑,把它们一个个封装起来, 并且使它们可相互替换。

#### 行为模式：

> 允许一个对象在其内部状态改变时改变它的行为，对象看起来似乎修改了它的类。

策略模式和状态模式确实是相似的，它们都封装行为、都通过委托来实现行为分发。
但策略模式中的行为函数是”潇洒“的行为函数，它们不依赖调用主体、互相平行、各自为政，井水不犯河水。而状态模式中的行为函数，首先是和状态主体之间存在着关联，由状态主体把它们串在一起；另一方面，正因为关联着同样的一个（或一类）主体，所以不同状态对应的行为函数可能并不会特别割裂。

#### 观察者模式（使用频率最高、面试频率最高）：

几乎可以称其为**发布-订阅模式**

- > 观察者模式定义了一种一对多的依赖关系，让多个观察者对象同时监听某一个目标对象，当这个目标对象的状态发生变化时，会通知所有观察者对象，使它们能够自动更新。

Vue中的发布订阅模式

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0ab7a4846d604721b6b91418ee97bf91~tplv-k3u1fbpfcp-watermark.awebp)

全局事件总线严格来说并不是观察者模式，而是发布订阅模式

**观察者模式与发布订阅模式的区别**

- 发布者直接触及到订阅者的操作，叫观察者模式
- 发布者通过第三方（事件中心）来完成实际的通信的操作，叫做发布订阅模式

#### 迭代器模式：

> 使我们在访问集合内每一个成员时不用去关心集合本身的内部结构以及集合与集合间的差异，这就是迭代器存在的价值

ES6对迭代器的实现：ES6约定，任何数据结构只要具备Symbol.Iterator属性，就可以被for...of和next遍历，事实上，for..of就是对next方法的反复调用

生成器(Generator)用于编写迭代器生成函数

## 
