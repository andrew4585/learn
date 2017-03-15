# boolean知识遗漏
### Boolean()方法转换
<table>
    <tr>
        <th>数据类型</th>
        <th>转换为true的值</th>
        <th>转换为false的值</th>
    </tr>
    <tr>
        <td>Boolean</td>
        <td>true</td>
        <td>false</td>
    </tr>
    <tr>
        <td>String</td>
        <td>任何非空字符串</td>
        <td>""(空字符串)</td>
    </tr>
    <tr>
        <td>Number</td>
        <td>任何非零数字（包括无穷大）</td>
        <td>0和NaN</td>
    </tr>
    <tr>
        <td>Object</td>
        <td>任何对象</td>
        <td>null</td>
    </tr>
    <tr>
        <td>Undefined</td>
        <td>n/a</td>
        <td>undefined</td>
    </tr>
<table>

> if语句自动执行相应的boolean转换
``` javascript
var message = "hello world";
if(message){
    alert("value is true");
}
```
## 布尔操作符
> 应用于任何操作类型，不仅仅是布尔类型

1. __逻辑与（&&）__

__遵循规则：__
* 第一个操作数是对象，则返回第二个操作数
* 第二个操作数是对象，则只有在第一个操作数的求值结果为true的情况下返回该对象
* 二个操作数都是对象，则返回第二个操作数
* 如果有一个操作数为null，则返回null
* 如果有一个操作数为NaN，则返回NaN
* 如果有一个操作数为undefined，则返回undefined

2. __逻辑非（||）__

__遵循规则：__
* 第一个操作数是对象，则返回第一个操作数
* 第一个操作数的求值结果是false，则返回第二个操作数
* 二个操作数都是对象，则返回第一个操作数
> 赋值语句可以利用逻辑非的特性，避免赋予null或undefined
