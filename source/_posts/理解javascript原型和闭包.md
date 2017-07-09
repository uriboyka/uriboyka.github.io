---
title: 理解javascript原型和闭包
date: 2017-04-17 22:41:59
tags:
  - javascript
  - 闭包
categories: JavaScript
---

* 值类型的类型判断用typeof，引用类型的类型判断用instanceof：
```javascript
function show(x) {

            console.log(typeof(x));    // undefined
            console.log(typeof(10));   // number
            console.log(typeof('abc')); // string
            console.log(typeof(true));  // boolean

            console.log(typeof(function () { }));  //function

            console.log(typeof([1, 'a', true]));  //object
            console.log(typeof ({ a: 10, b: 20 }));  //object
            console.log(typeof (null));  //object
            console.log(typeof (new Number(10)));  //object
        }
        show();
```

* 一切（引用类型）都是对象，对象是属性的集合。

* 一切对象都是通过函数来创建的：
```javascript
        //var obj = { a: 10, b: 20 };
        //var arr = [5, 'x', true];

        var obj = new Object();
        obj.a = 10;
        obj.b = 20;

        var arr = new Array();
        arr[0] = 5;
        arr[1] = 'x';
        arr[2] = true;
```

* 每个函数都有一个属性叫做prototype。这个prototype的属性值是一个对象（属性的集合，再次强调！），默认的只有一个叫做constructor的属性，指向这个函数本身。

* 每个对象都有一个隐藏的属性——“\__proto\__”，这个属性引用了创建这个对象的函数的prototype。即：fn.\__proto\__ === Fn.prototype。

* 每个函数function都有一个prototype，即原型。这里再加一句话——每个对象都有一个\__proto\__，可成为隐式原型。

* 每个对象都有一个\__proto\__属性，指向创建该对象的函数的prototype(原型)。

* Object.prototype确实一个特例——它的\__proto\__指向的是null，切记切记！

* “f1 instanceof Object” Instanceof的判断队则是：沿着A的\__proto\__这条线来找，同时沿着B的prototype这条线来找，如果两条线能找到同一个引用，即同一个对象，那么就返回true。如果找到终点还未重合，则返回false。

* 访问一个对象的属性时，先在基本属性中查找，如果没有，再沿着\__proto\__这条链向上找，这就是原型链。
---
* 在函数中this到底取何值，是在函数真正被调用执行的时候确定的，函数定义的时候确定不了。

* this的取值分四种情况：
    1. 如果函数作为构造函数，this就代表它即将new出来的对象；如果直接调用，this是window。
    2. 如果函数作为对象的一个属性时，**并且作为对象的一个属性被调用时**，函数中的this指向该对象。
    3. 如果函数被call和apply调用时，this的值就取传入的对象的值。
    4. 全局环境和普通函数在调用时，其中的this也都是window。


* javascript没有块级作用域--javascript除了全局作用域之外，只有函数可以创建的作用域。

* 我们在声明变量时，全局代码要在代码前端声明，函数中要在函数体一开始就声明好。除了这两个地方，其他地方都不要出现变量声明。而且建议用“单var”形式。

* 作用域最大的用处就是隔离变量，不同作用域下同名变量不会有冲突。

* 除了全局作用域之外，每个函数都会创建自己的作用域，作用域在函数定义时就已经确定了。而不是在函数调用时确定。

* 作用域中变量的值是在执行过程中产生的确定的，而作用域却是在函数创建时就确定了。所以，如果要查找一个作用域下某个变量的值，就需要找到这个作用域对应的执行上下文环境，再在其中寻找变量的值。

* 闭包应用的两种情况：函数作为返回值，函数作为参数传递。
---
* 所有的对象都有"\__proto\__"属性，该属性对应该对象的原型

* 所有的函数对象都有"prototype"属性，该属性的值会被赋值给该函数创建的对象的"\__proto\__"属性

* 所有的原型对象都有"constructor"属性，该属性对应创建所有指向该原型的实例的构造函数

* 函数对象和原型对象通过"prototype"和"constructor"属性进行相互关联
