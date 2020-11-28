# TypeScript

## 什么是TypeScript

[TypeScript](http://www.typescriptlang.org/) 是 JavaScript 的一个超集，主要提供了**类型系统**和**对 ES6 的支持**，它由 Microsoft 开发，代码[开源于 GitHub](https://github.com/Microsoft/TypeScript) 上。 

#### 安装&编译TypeScript

npm install -g typescript

tsc hello.ts

我们约定使用 TypeScript 编写的文件以 `.ts` 为后缀，用 TypeScript 编写 React 时，以 `.tsx` 为后缀。 

## 原始数据类型

JavaScript 的类型分为两种：原始数据类型（[Primitive data types](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)）和对象类型（Object types）。 

原始数据类型包括：布尔值、数值、字符串、`null`、`undefined` 以及 [ES6 中的新类型 `Symbol`](http://es6.ruanyifeng.com/#docs/symbol) 

***布尔值***

````
let isDone: boolean = false;  
````

 注意，使用构造函数 `Boolean` 创造的对象**不是**布尔值

事实上 `new Boolean()` 返回的是一个 `Boolean` 对象： let createdByNewBoolean: Boolean = new Boolean(1);

直接调用 `Boolean` 也可以返回一个 `boolean` 类型： let createdByBoolean: boolean = Boolean(1); 

***数值***

````
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
// ES6 中的二进制表示法
let binaryLiteral: number = 0b1010;
// ES6 中的八进制表示法
let octalLiteral: number = 0o744;
let notANumber: number = NaN;
let infinityNumber: number = Infinity;
````

***字符串***

````
let myName: string = 'Tom';
let myAge: number = 25;

// 模板字符串
let sentence: string = `Hello, my name is ${myName}.
I'll be ${myAge + 1} years old next month.`;
````

***空值***

JavaScript 没有空值（Void）的概念，在 TypeScript 中，可以用 `void` 表示没有任何返回值的函数： 

~~~~
function alertName(): void {
    alert('My name is Tom');
}
~~~~

声明一个 `void` 类型的变量没有什么用，因为你只能将它赋值为 `undefined` 和 `null` 

~~~~

~~~~

***Null和Undefined***

在 TypeScript 中，可以使用 `null` 和 `undefined` 来定义这两个原始数据类型： 

~~~~

~~~~

与 `void` 的区别是，`undefined` 和 `null` 是所有类型的子类型。也就是说 `undefined` 类型的变量，可以赋值给 `number` 类型的变量： 

~~~~
// 这样不会报错
let num: number = undefined;
// 这样也不会报错
let u: undefined;
let num: number = u;
~~~~

而 `void` 类型的变量不能赋值给 `number` 类型的变量： 

~~~~
let u: void;
let num: number = u;

// Type 'void' is not assignable to type 'number'.
~~~~

## 任意值

任意值（Any）用来表示允许赋值为任意类型。 

如果是一个普通类型，在赋值过程中改变类型是不被允许的： 

~~~~

~~~~

但如果是 `any` 类型，则允许被赋值为任意类型。 

~~~~
let myFavoriteNumber: any = 'seven';
myFavoriteNumber = 7;
~~~~

任意值的属性和方法

在任意值上访问任何属性是允许的：

~~~~

~~~~

也允许调用任何方法：

~~~~

~~~~

也可以认为，**声明一个变量为任意值之后，对它的任何操作，返回的内容都是任意值**

未声明类型的变量

**变量如果在声明的时候，未指定其类型，那么它会被识别为任意值类型**： 

~~~~

~~~~

等价于：

~~~~

~~~~

## 类型推论

如果没有明确的指定类型，那么 TypeScript 会依照类型推论（Type Inference）的规则推断出一个类型。 

TypeScript 会在没有明确的指定类型的时候推测出一个类型，这就是类型推论。

**如果定义的时候没有赋值，不管之后有没有赋值，都会被推断成** `any` **类型而完全不被类型检查**：

~~~~
let myFavoriteNumber;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
~~~~

## 联合类型

联合类型（Union Types）表示取值可以为多种类型中的一种

~~~~

~~~~

当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候，我们**只能访问此联合类型的所有类型里共有的属性或方法**： 

~~~~

~~~~

联合类型的变量在被赋值的时候，会根据类型推论的规则判断出一个类型：

~~~~typescript

~~~~

上例中，第二行的 `myFavoriteNumber` 被推断成了 `string`，访问它的 `length` 属性不会报错。

而第四行的 `myFavoriteNumber` 被推断成了 `number`，访问它的 `length` 属性时就报错了。

