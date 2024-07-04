# #类对象的结构

对象中存储属性的区域实际有两个

1. 对象自身

   - 直接通过对象所添加的属性，位于对象自身中

   - 在类中通过 x=y 的形式添加的属性，也位于对象自身中

2. **原型对象（prototype）**
   - 对象中有一个属性用来存储原型对象，这个属性叫做**proto**
   - 原型对象也负责为对象储存属性
     - 当我们访问对象中的属性时，**会优先访问对象自身的属性**。
     - 对象自身不包含该属性时，才会去原型对象中寻找。
   - 会添加到原型对象中的情况
     - **在类中通过 xxx(){}方式添加的方法，位于原型中**
     - 主动向原型中添加的属性或方法

<img src="/Users/zhangzhuang/Desktop/front-learn/javascript-oo-feature-对象的结构 10.assets/image-20240617095841814.png" alt="image-20240617095841814" style="zoom:40%;" />

> 为啥要有些成员变量要存放在原型对象中呢？

## 原型对象 - prototype

访问一个对象的原型对象

- **对象.\_\_proto\_\_**
- **Object.getPrototypeOf( 对象 ) **

原型对象中的数据

1. 对象中的数据，包括属性，方法等
2. constructor 构造函数

注意：

原型对象也有原型，这样就构成了一条原型链，根据对象的复杂程度不同，原型链的长度也不同

自己创建的 p 对象的原型链：类对象 -> 原型 -> 原型 -> null

```javascript
class Person {
  name;
  age;
  sayHello() {
    console.log('Hello,我是 ' + this.name);
  }
}
```

空对象的原型链：obj 对象 -> 原型 -> null

```js
const obj = {};
```

​ 原型链：

- 读取对象属性时，会优先从对象自身属性

  如果对象中有，则使用，没有则去对象的原型中寻找

​ 如果原型中有，则使用，没有则去原型的原型中寻找

直到找到 Object 对象的原型，如果依然没有找到，则返回**undefined**

- 作用域链，是找变量的链，找不到会报错
- 原型链，是找属性的链，找不到会返回 undefined

**所有同类型对象他们的原型对象是相同的。如图所示：**

<img src="/Users/zhangzhuang/Desktop/front-learn/javascript-oo-feature-对象的结构 10.assets/image-20240618094741789.png" alt="image-20240618094741789" style="zoom:50%;" />

原型的作用：将成员方法统一存储到公共区域，节约内存。比如有 100 个类对象，每个对象都含有方法 sayHello，其功能都是一样的，那么就可以将这个方法放到原型对象中。

继承的原理：更改子类的原型对象为父类。

Cat 对象的原型链为：

**<u>cat 对象——> Animal</u>** ——> object ——> Object ——> Object 原型 ——> null

```js
class Animal {}
class Cat extends Animal {}
class Tomcat extends Cat {}
const cat = new Cat();
```

## 如何修改原型

大部分情况下，我们是不需要修改原型对象的。
