### Symbol

ES6引入的一种新的原始数据类型Symbol，表示独一无二的值。

- 它是JavaScript语言的第七种数据类型，前六种是：Undefined、Null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。

- Symbol值通过Symbol函数生成。

    注意，Symbol函数前不能使用new命令，否则会报错。这是因为生成的Symbol是一个原始类型的值，不是对象。
    也就是说，由于Symbol值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。
    
- Symbol函数可以接受一个字符串作为参数，表示对Symbol实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分。

- Symbol值不能与其他类型的值进行运算，会报错。

- Symbol值可以显式转为字符串，Symbol值也可以转为布尔值，但是不能转为数值。

#### 作为属性名的Symbol

由于每一个Symbol值都是不相等的，这意味着Symbol值可以作为标识符，用于对象的属性名，就能保证不会出现同名的属性。这对于一个对象由多个模块构成的情况非常有用，能防止某一个键被不小心改写或覆盖。

    注意，Symbol值作为对象属性名时，不能用点运算符。
    
在对象的内部，使用Symbol值定义属性时，Symbol值必须放在方括号之中。

Symbol类型还可以用于定义一组常量，保证这组常量的值都是不相等的。


#### 属性名的遍历

Symbol作为属性名，该属性不会出现在 `for...in` 、 `for...of` 循环中，也不会被 `Object.keys()` 、 `Object.getOwnPropertyNames()` 返回。

但是，它也不是私有属性，有一个 `Object.getOwnPropertySymbols` 方法，可以获取指定对象的所有Symbol属性名的数组。

`Reflect.ownKeys` 方法可以返回所有类型的键名，包括常规键名和Symbol键名。

#### Symbol.for()

它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的Symbol值。如果有，就返回这个Symbol值，否则就新建并返回一个以该字符串为名称的Symbol值。Symbol.for()生成的值会被登记在全局环境中供搜索。

#### Symbol.keyFor()

Symbol.keyFor方法返回一个已登记的Symbol类型值的key。

```javascript
var s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"

var s2 = Symbol("foo");
Symbol.keyFor(s2) // undefined
```

#### 内置的Symbol值

- 对象的 `Symbol.hasInstance` 属性，指向一个内部方法。当其他对象使用 `instanceof` 运算符，判断是否为该对象的实例时，会调用这个方法。

- 对象的 `Symbol.isConcatSpreadable` 属性等于一个布尔值，表示该对象使用 `Array.prototype.concat()` 时，是否可以展开。

- 对象的 `Symbol.species` 属性，指向一个方法。该对象作为构造函数创造实例时，会调用这个方法。

- 对象的 `Symbol.match` 属性，指向一个函数。当执行 `str.match(myObject)` 时，如果该属性存在，会调用它，返回该方法的返回值。

- 对象的 `Symbol.replace` 属性，指向一个方法，当该对象被 `String.prototype.replace` 方法调用时，会返回该方法的返回值。

- 对象的 `Symbol.search` 属性，指向一个方法，当该对象被 `String.prototype.search` 方法调用时，会返回该方法的返回值。

- 对象的 `Symbol.split` 属性，指向一个方法，当该对象被 `String.prototype.split` 方法调用时，会返回该方法的返回值。

- 对象的 `Symbol.iterator` 属性，指向该对象的默认遍历器方法。

- 对象的 `Symbol.toPrimitive` 属性，指向一个方法。该对象被转为原始类型的值时，会调用这个方法，返回该对象对应的原始类型值。

- 对象的 `Symbol.toStringTag` 属性，指向一个方法。在该对象上面调用 `Object.prototype.toString` 方法时，如果这个属性存在，它的返回值会出现在 `toString` 方法返回的字符串之中，表示对象的类型。

- 对象的 `Symbol.unscopables` 属性，指向一个对象。该对象指定了使用 `with` 关键字时，哪些属性会被 `with` 环境排除。
