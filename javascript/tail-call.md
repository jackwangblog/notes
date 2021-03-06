### 尾调用
尾调用是指一个函数里的最后一步操作是函数调用的情形。若函数最后一步调用的函数是自己，则叫做尾递归。“尾”不是指物理位置上的尾部，而是指最后一步操作。

```javascript
function foo() {
    return bar();
}

function foo(arg) {
    if (arg) {
        // 如果arg是true，这里将执行一个尾调用
        return a();
    }
    // 最后一步是+1，所以这种情况不是尾调用
    return b() + 1;
}
```
### 需要了解的一个概念 调用帧
当程序执行某个函数(或方法)时，会从栈中分配一块内存空间，这块内存空间我们叫做帧。它用来保存函数里的变量的值，记录调用位置，并被放入栈中。当函数里再调用了其他函数时，便会在栈中形成一个帧序列。被调用的函数执行完后，对应的帧会从栈中弹出并释放。

### 尾调用优化
尾调用因为是函数的最后一步操作，不需要再使用外层函数的局部变量，调用位置等信息，所以这些信息就不需要再保存了，此时这个帧就可以释放了。最明显的场景就是递归调用了。递归次数越多，需要保存的调用记录就越多，如果使用了尾调用优化，就只需要保存一个记录。

### ES6已实现，需要在严格模式下使用
http://www.ecma-international.org/ecma-262/6.0/index.html#sec-tail-position-calls

### 参考链接
https://zh.wikipedia.org/zh-cn/%E5%B0%BE%E8%B0%83%E7%94%A8
http://www.ruanyifeng.com/blog/2015/04/tail-call.html
