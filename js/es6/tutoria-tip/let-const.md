## let 和 const 命令

#### let 命令

* 作用域

    只在let命令所在的代码块内有效
* 不能重复声明变量
* let在for循环中的作用域

    *for循环还有一个特别之处，就是循环语句部分是一个父作用域，而循环体内部是一个单独的子作用域*

    ``` javascript
    for (let i = 0; i < 3; i++) {
      let i = 'abc';
      console.log(i);
    }
    // abc
    // abc
    // abc
    ```

#### 块级作用域

* ES5 只有全局作用域和函数作用域，没有块级作用域

* ES6 的块级作用域

    ``` javascript
    function f1() {
      let n = 5;
      if (true) {
        let n = 10;
      }
      console.log(n); // 5
    }
    ```
* 块级作用域的出现，实际上使得获得广泛应用的立即执行函数表达式（IIFE）不再必要了。

    ``` javascript
    // IIFE 写法
    (function () {
      var tmp = ...;
      ...
    }());

    // 块级作用域写法
    {
      let tmp = ...;
      ...
    }```

#### 块级作用域与函数声明

* 注意点：ES6浏览器与其他环境遵循的规则不同，详见教程

#### const 命令

* const声明一个只读的常量。一旦声明，常量的值就不能改变
* const的作用域与let命令相同：只在声明所在的块级作用域内有效

    **本质：const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动**

    ``` javascript
    const foo = {};

    // 为 foo 添加一个属性，可以成功
    foo.prop = 123;
    foo.prop // 123

    // 将 foo 指向另一个对象，就会报错
    foo = {}; // TypeError: "foo" is read-only

    ```

    ``` javascript
    const a = [];
    a.push('Hello'); // 可执行
    a.length = 0;    // 可执行
    a = ['Dave'];    // 报错

    ```
