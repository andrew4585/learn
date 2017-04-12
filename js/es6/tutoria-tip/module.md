## Module

### 1.概述
* 静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量
* ES6 模块不是对象，而是通过export命令显式指定输出的代码，再通过import命令输入

    ``` javascript
    // ES6模块
    import { stat, exists, readFile } from 'fs';
    ```
* 严格模式
* 模块功能主要由两个命令构成：`export` 和 `import`

### 2.export 命令

* 概念

    一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量

    ``` javascript
    // profile.js
    export var firstName = 'Michael';
    export var lastName = 'Jackson';
    export var year = 1958;

    //另一种写法
    // profile.js
    var firstName = 'Michael';
    var lastName = 'Jackson';
    var year = 1958;
    export {firstName, lastName, year};
    ```

* 可输出类型：变量，函数，类（Class）

    ``` javascript
    function v1() { ... }
    function v2() { ... }

    //可以使用as关键字重命名
    //重命名后，v2可以用不同的名字输出两次。
    export {
      v1 as streamV1,
      v2 as streamV2,
      v2 as streamLatestVersion
    };
    ```
* 错误写法

    ``` javascript
    // 报错
    export 1;

    // 报错
    var m = 1;
    export m;

    // 报错
    function f() {}
    export f;
    ```

* export命令可以出现在模块的任何位置，只要处于模块顶层就可以.如果处于块级作用域内，就会报错

### 3.import命令
* 语法
    ``` javascript
    // main.js
    import {firstName as a, lastName, year} from './profile';
    ```

* 可使用as重命名
* 如果只是模块名，不带有路径，那么必须有配置文件

    ``` javascript
    import {myMethod} from 'util';
    ```
* import命令具有提升效果，会提升到整个模块的头部，首先执行
* import是静态执行，所以不能使用表达式和变量

    ``` javascript
    // 报错
    import { 'f' + 'oo' } from 'my_module';

    // 报错
    let module = 'my_module';
    import { foo } from module;

    // 报错
    if (x === 1) {
      import { foo } from 'module1';
    } else {
      import { foo } from 'module2';
    }
    ```
* 整体加载

    ``` javascript
    // circle.js
    export function area(radius) {
      return Math.PI * radius * radius;
    }
    export function circumference(radius) {
      return 2 * Math.PI * radius;
    }

    // main.js
    import * as circle from './circle';
    console.log('圆面积：' + circle.area(4));
    console.log('圆周长：' + circle.circumference(14));
    ```
* import default命令
    1. import 无需有大括号
    2. 一个模块只能有一个默认输出
    3. 同时输入默认方法和其他变量
    ``` javascript
        import _, { each } from 'lodash';
    ```

### 4.export 与 import 的复合写法
### 5.模块的继承
### 6.跨模块常量
### 7.import()
