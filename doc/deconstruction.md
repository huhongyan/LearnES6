### 变量的解构赋值

ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。如果解构不成功，变量的值就等于undefined。

解构赋值不仅适用于 `var` 命令，也适用于 `let` 和 `const` 命令。


#### 默认值

解构赋值允许指定默认值

    注意，ES6内部使用严格相等运算符（===），判断一个位置是否有值。
    所以，如果一个数组成员(对象的属性值)不严格等于undefined，默认值是不会生效的。
    
如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候，才会求值。

默认值可以引用解构赋值的其他变量，但该变量必须已经声明。

#### 数组的解构赋值

从数组中提取值，按照对应位置，对变量赋值。

- 如果等号的右边不是数组（或者严格地说，不是可遍历的结构），那么将会报错。

- 对于Set结构，也可以使用数组的解构赋值。事实上，只要某种数据结构具有Iterator接口，都可以采用数组形式的解构赋值。


#### 对象的解构赋值

对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

- 如果变量名与属性名不一致，必须写成下面这样。

```javascript
var { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"

let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
f // 'hello'
l // 'world'
```
对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。

    注意，采用这种写法时，变量的声明和赋值是一体的。
    对于let和const来说，变量不能重新声明，所以一旦赋值的变量以前声明过，就会报错。
    
```javascript
let foo;
({foo} = {foo: 1}); // 成功

let baz;
({bar: baz} = {bar: 1}); // 成功
```
- 上面代码中，`let` 命令下面一行的圆括号是必须的，否则会报错。因为解析器会将起首的大括号，理解成一个代码块，而不是赋值语句。

- 和数组一样，解构也可以用于嵌套结构的对象。

- 如果解构模式是嵌套的对象，而且子对象所在的父属性不存在，那么将会报错。

```javascript
// 报错
var {foo: {bar}} = {baz: 'baz'};
```

- 解构赋值允许，等号左边的模式之中，不放置任何变量名。

- 对象的解构赋值，可以很方便地将现有对象的方法，赋值到某个变量。

```javascript
let { log, sin, cos } = Math;
```

- 由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

```javascript
var arr = [1, 2, 3];
var {0 : first, [arr.length - 1] : last} = arr;
first // 1
last // 3
```

#### 字符串的解构赋值

字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。

#### 数值和布尔值的解构赋值

解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。

解构赋值的规则是，只要等号右边的值不是对象，就先将其转为对象。由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。

#### 函数参数的解构赋值

```javascript
function add([x, y]){
  return x + y;
}

add([1, 2]); // 3
```

#### 圆括号问题

建议只要有可能，就不要在模式中放置圆括号。

- 以下三种解构赋值不得使用圆括号。

    + 变量声明语句中，不能带有圆括号。
    
    + 函数参数中，模式不能带有圆括号。
    
    + 赋值语句中，不能将整个模式，或嵌套模式中的一层，放在圆括号之中。
    
- 可以使用圆括号的情况只有一种：赋值语句的非模式部分，可以使用圆括号。

#### 用途

- 交换变量的值

- 从函数返回多个值

- 函数参数的定义

- 提取JSON数据

- 函数参数的默认值

- 遍历Map结构

- 输入模块的指定方法
