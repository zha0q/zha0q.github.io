---
title: TypeScript
author: zq
date: 2021-10-24
category: contest
layout: post
---


#### TS类型编程为什么叫做类型体操？

1. TypeScript 给 JavaScript 增加了一套静态类型系统，通过 TS Compiler 编译为 JS，编译的过程做类型检查。

   它并没有改变 JavaScript 的语法，只是在 JS 的基础上添加了类型语法，所以被叫做 JavaScript 的超集。

   JavaScript 的标准在不断的发展，TypeScript 的类型系统也在不断完善，因为“超集”的设计理念，这两者可以很好的融合在一起，是不会有冲突的。

2. 三种类型系统

   - 简单类型系统

   - 支持泛型的类型系统
   - 支持类型编程的类型系统

#### TS类型和类型运算

1. 类型

   -  number、boolean、string、object、bigint、symbol、undefined、null 这些类型，还有就是它们的包装类型 Number、Boolean、String、Object、Symbol。
   - 元组：元素个数和类型**固定**的数组类型
   - `接口（Interface）`可以描述函数、对象、构造器的结构
   - `枚举（Enum）`是一系列值的复合
   - **void** 代表空，可以是 null 或者 undefined，一般是用于函数返回值。
   - **any** 是任意类型，任何类型都可以赋值给它，它也可以赋值给任何类型（除了 never）。
   - **unknown** 是未知类型，任何类型都可以赋值给它，但是它不可以赋值给别的类型。
   - **never** 代表不可达，比如函数抛异常的时候，返回值就是 never。

2. 类型装饰

   ```typescript
   interface IPerson {
       readonly name: string;
       age?: number;
   }
   ```

   

3. 类型运算
   - 条件类型 extends ? :
   - 推导 infer
   - 联合 |
   - 交叉 &
   - 映射 :  因为 js 处理对象比较多，所以索引类型的映射比较重要。
     - keyof T 是查询索引类型中所有的索引，叫做`索引查询`。
     - T[Key] 是取索引类型某个索引的值，叫做`索引访问`。
     - in 是用于遍历联合类型的运算符。



#### type和interface不同点

1. type 用 交叉类型`&` 继承，interface用extends实现继承
2. type可以定义基本类型别名
3. type可以通过typeof操作符定义
4. type声明联合类型
5. type声明元组类型
6. interface可以进行声明合并



#### 泛型

1. 为什么需要泛型：一个组件支持多种类型的数据，这样用户就可以以自己的数据类型来使用组件

2. 语法 `<T> `

3. 处理函数副作用

   ```typescript
   interface UserInfo {
       name: string
       age: number
   }
   
   function request<T>(url:string): Promise<T> {
       return fetch(url).then(res => res.json())
   }
   
   request<UserInfo>('user/info').then(res =>{
       console.log(res)
   })
   
   ```

4. 泛型应用

   - 泛型约束类（无法约束类的静态成员）

   - 泛型约束接口

     ```typescript
     interface IKeyValue<T, U> {
         key: T
         value: U
     }
     
     const k1:IKeyValue<number, string> = { key: 18, value: 'lin'}
     const k2:IKeyValue<string, number> = { key: 'lin', value: 18}
     
     ```

   - 实战：泛型约束后端接口参数

     ```typescript
     import axios from 'axios'
     
     interface API {
         '/book/detail': {
             id: number,
         },
         '/book/comment': {
             id: number
             comment: string
         }
         ...
     }
     
     
     function request<T extends keyof API>(url: T, obj: API[T]) {
         return axios.post(url, obj)
     }
     
     request('/book/comment', {
         id: 1,
         comment: '非常棒！'
     })
     
     ```

     



#### 套路一、模式匹配做提取

- TypeScript 类型的模式匹配是通过类型 extends 一个模式类型，把需要提取的部分放到通过 infer 声明的局部变量里，后面可以从这个局部变量拿到类型做各种后续处理。

#### 套路二、重新构造做变换

- TypeScript 支持 type、infer、类型参数来保存任意类型，相当于变量的作用。

  但其实也不能叫变量，因为它们是不可变的。**想要变化就需要重新构造新的类型，并且可以在构造新类型的过程中对原类型做一些过滤和变换。**



#### 套路三、递归复用做循环

- 在 TypeScript 类型系统中的高级类型也同样支持递归，**在类型体操中，遇到数量不确定的问题，要条件反射的想到递归。** 比如数组长度不确定、字符串长度不确定、索引类型层数不确定等。

#### 套路四、数组长度做计数

- ```typescript
  type BuildArray<
      Length extends number, 
      Ele = unknown, 
      Arr extends unknown[] = []
  > = Arr['length'] extends Length 
          ? Arr 
          : BuildArray<Length, Ele, [...Arr, Ele]>;
  ```

  

