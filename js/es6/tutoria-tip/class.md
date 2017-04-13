## Class
#### 1.class基本语法

* 概念
> ES6的类，完全可以看作构造函数的另一种写法

    ``` javascript
    function Point(x, y) {
      this.x = x;
      this.y = y;
    }

    Point.prototype.toString = function () {
      return '(' + this.x + ', ' + this.y + ')';
    };

    var p = new Point(1, 2);
    // ---------------------------
    //等价
    class Point {
      constructor(x, y) {
        this.x = x;
        this.y = y;
      }

      toString() {
        return '(' + this.x + ', ' + this.y + ')';
      }
    }
    typeof Point // "function"
    Point === Point.prototype.constructor // true
    ```

* constructor方法是类的默认方法
* Class不存在变量提升（hoist），这一点与ES5完全不同
* this的指向
> 类的方法内部如果含有this，它默认指向类的实例

#### 2.class继承

* 基本用法

    > Class之间可以通过extends关键字实现继承

    ``` javascript
    class ColorPoint extends Point {}
    ```

* 调用父类
``` javascript
class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y); // 调用父类的constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }
}
```
> 子类必须在constructor方法中调用super方法，否则新建实例时会报错

* super语法

    * super作为函数调用时，代表父类的构造函数
    >作为函数时，super()只能用在子类的构造函数之中，用在其他地方就会报错
    * super作为对象时，在普通方法中，指向父类的原型对象；在静态方法中，指向父类
        * 由于super指向父类的原型对象，所以定义在父类实例上的属性，是无法通过super调用的
        * 如果通过super对某个属性赋值，这时super就是this
        ``` javascript
        class A {
            constructor() {
                this.x = 1;
            }
        }

        class B extends A {
            constructor() {
                super();
                this.x = 2;
                super.x = 3;    //等同于this.x=3;
                console.log(super.x); // undefined
                console.log(this.x); // 3
            }
        }
        ```

#### 3.Class的取值函数（getter）和存值函数（setter）

``` javascript
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'
```

#### 4.Class 的 Generator 方法
#### 5.Class 的静态方法
``` javascript
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod() // 'hello'

var foo = new Foo();
foo.classMethod()
// TypeError: foo.classMethod is not a function
```
* 静态方法可被子类继承
* 静态方法也是可以从super对象上调用的。
