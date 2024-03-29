# JS原型链 :__proto__与prototype

JS的原型链是JS最难理解的知识点之一，但是它又是极其重要的，因为如果不懂原型，将会很难真正的理解其他概念。
## 1. 什么是```__proto__```
但其实它的内容并不多，几句话可以说完:
1. 只要是对象，他就会有一个```__proto__```
2. ```__proto__```里面存着一个地址，指向另一个对象，所以可以错误地理解为```__proto__```也是一个对象（准确的说，它是存储着一个对象的地址），它会引用构造它的函数的```prototype```，也就是原型
3. 所以既然```__proto__```是一个对象，那么它也会有```__proto__```
4. 为什么称为原型链，就是这个原因，因为原型的原型还会有原型
5. 那么既然是个链，那如果把一开始的对象出发，看做是起点的话，它必须有一个终点，它就是```Object.prototype```。他就是原型链的根对象，因为它的```__proto__```的值为null。
6. 只要是个对象，沿着原型链找下去，最后都会到达跟对象。

## 2. 什么是```prototype```
好了，关于```__proto__```的内容就讲完了，但是```prototype```又是什么东西呢？？？其实也很好理解：
1. 只要是函数就存在一个```prototype```。它也指向一个地址，会被所构造的对象的```__proto__```所引用。
2. 所以有这么一个等式：
``` obj.__proto__===构造它的函数.prototype```
3. 意思就是说``` obj.__proto__```与```构造它的函数.prototype```所指向的地址指向同一个对象，也就是原型。
## 3. 总结
上面这两段话还是有点多，可以浓缩为：

**1. 所有对象都会有一个```__proto__```，它存着一个地址，指向构造它的函数的```prototype```，也就是原型，原型也是一个对象**

**2. 所有的函数都有一个```prototype```,会被它所构造的函数的对象所引用**

**3. 一个重要的等式：``` obj.__proto__===构造它的函数.prototype```**

**4. 原型链是层层相连的，它存在一个终点，也就是根对象，为```Object.prototype```，它的```__proto__```的值为null**
## 4. 拓展
看完了前面三点，基本的原型链的问题都可以理解了，但是还可以进一步深入的思考。
*1. Object()也是一个函数，那么它的 ```__proto__``` 引用的是哪个 ```prototype``` 的地址呢？换个问法，Object()是由谁构造的呢？*

这个问题比较好回答，只要是函数，都是由Function()构造的，所以它指向的是：```Function.prototype```，即``` Object.__proto__===Function.prototype```

*2. 那么Function()是由谁所构造的呢？？？*

既然Function()也是一个函数，那么他也是由Function所构造的。这听起来有点拗口：我生了我自己？？？大家不必去纠结这个伦理问题，真正的原因是：浏览器构造了Function，然后强行指定了，它的```__proto__``` 引用了它的```prototype```。即``` Function.__proto__===Function.prototype```

*3. 既然 ```Object.prototype``` 才是根对象，但是 ```Object.__proto__``` 又引用了 ```Function.prototype``` ,那是不是很奇怪呢？说好的最后是回到根对象的呀！*

解决这个问题，要记住一点：**原型也是一个对象！**
既然原型也是一个对象，那么它也会有```__proto__```,所以```Object.__proto__```引用了```Function.prototype```，```Function.prototype.__proto__```又引用了```Object.prototype```，这不就回到了根对象了吗。
可以有下面等式：
```js
Object.__proto__===Function.prototype
Function.prototype.__proto__===Object.prototype
//上面两个等式合起来
Object.__proto__.__proto__===Object.prototype
```
这就完美地解答了这个疑问。
