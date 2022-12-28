<p align="center">
  <img src="https://raw.githubusercontent.com/rmolinamir/typescript-cheatsheet/master/TypeScript.png" alt="TypeScript"/>
</p>

# TypeScript 

A set of TypeScript related notes used for quick reference. The cheatsheet contains references to types, classes, decorators, and many other TypeScript related subjects.

## Introduction

TypeScript is a very powerful addition to JavaScript. TypeScript is developed by Microsoft and is increasingly supported by the day  by technologies such as Angular, Vue.js 3, React.js, and many others.

As TypeScript code can be compiled to ES5, it includes all of the native JavaScript features such as spread arrow function, deconstructors, and introduces some **very** useful features such as decorators, generics and interfaces, enums, modules, among others which can be found in different programming languages.

TypeScript is not an entirely new language it’s a superset of JavaScript so that means any valid JavaScript code is also valid TypeScript code but TypeScript has additional features that do not exist in current version of JavaScript.

### TypeScript Concepts

Strong or static typing — such as in languages like C# and Java when we define variables we need to specify the type of that variable.
Object-oriented features — that was not in Javascript. Now we have the concept of classes, interfaces, constructors, access modifiers like public and private available in Typescript.
Compile-time errors — we can catch errors at compile time instead of at runtime — not all kind of errors but a lot of errors. We can catch these errors at compile time and fix them before deploying our application.

<br>

---

## Types

> For programs to be useful, we need to be able to work with some of the simplest units of data: numbers, strings, structures, boolean values, and the like. In TypeScript, we support much the same types as you would expect in JavaScript, with a convenient enumeration type thrown in to help things along.

<br>

### Basic Assign Types

#### String

> Another fundamental part of creating programs in JavaScript for webpages and servers alike is working with textual data. As in other languages, we use the type string to refer to these textual datatypes. Just like JavaScript, TypeScript also uses double quotes (") or single quotes (') to surround string data.

```ts
  const myName: string = 'Robert';
```

<br>

#### Number

> As in JavaScript, all numbers in TypeScript are floating point values. These floating point numbers get the type `number`. In addition to hexadecimal and decimal literals, TypeScript also supports binary and octal literals introduced in ECMAScript 2015.

```ts
  const myAge: number = 24;
```

<br>

#### Boolean

> The most basic datatype is the simple `true`/`false` value, which JavaScript and TypeScript call a `boolean` value.

```ts
  const bHasHobbies: boolean = true;
```

<br>

#### Array

> TypeScript, like JavaScript, allows you to work with arrays of values. Array types can be written in one of two ways. In the first, you use the type of the elements followed by [] to denote an array of that element type:

```ts
  const hobbies: string[] = ['Programming', 'Cooking'];
```

If no types are declared, TypeScript will automatically assign a type depending on the types of the Array values.

```ts
  const numbers = [1, 3.22, 6, -1] // This variable will automatically be assigned a number[] array type.
```

**Note that declaring types is encouraged**.

<br>

### Tuples

> Tuple types allow you to express an array where the type of a fixed number of elements is known, but need not be the same. For example, you may want to represent a value as a pair of a `string` and a `number`:

```ts
  const address: [string, number] = ["Street", 99];
```

<br>

### Any

> We may need to describe the type of variables that we do not know when we are writing an application. These values may come from dynamic content, e.g. from the user or a 3rd party library. In these cases, we want to opt-out of type-checking and let the values pass through compile-time checks. To do so, we label these with the `any` type:

```ts
  let myCar: any = 'BMW';

  console.log(myCar); // Prints: BMW

  myCar = { brand: 'BMW', series: 3 };

  console.log(myCar) // Prints: { brand: "BMW", series: 3 }
```

<br>

### Enums

> A helpful addition to the standard set of datatypes from JavaScript is the enum. As in languages like C#, an enum is a way of giving more friendly names to sets of numeric values.
By default, any `enum` will begin numbering their members starting at 0. You can change this by manually setting the value of one of its members. For example, we can modify the Green value to 100, the next will be 101, then set Yellow back to 2.

```ts
  enum Color {
    Gray, // 0
    Red, // 1
    Green = 100, // 100
    Blue, // 101
    Yellow = 2 // 2
  }

  const myColor: Color = Color.Green
  console.log(myColor); // Prints: 100
```<br>

### Functions

Functions as you may expect work exactly the same as in JavaScript with a couple new features. In TypeScript, you may assign the function two things:

- Argument types.
- Function types.

```ts
  function returnMyName(myName): string {
    return myName;
  }

  console.log(returnMyName('Robert')) // Prints: Robert
```
<br>

### Argument Types

In TypeScript any argument of a function may be assigned a type no matter how complex, for example:

```ts
  // argument types
  function multiply(value1: number, value2: number) {
    return value1 * value2;
  }

  // console.log(multiply('Robert', 5)) // Not possible, both arguments must be of type number.
  console.log(multiply(10,5)) // Prints: 50
```
<br>

### Function Types

Just like the argument, the **return value** of a function may be assigned a type. Consider the example above to be included into the example below:

```ts
  const myMultiply: (val1: number, val2: number) => number;
  // myMultiply = sayHello; // Not possible.
  // myMultiply(); // Not possible.
  myMultiply = multiply;

  console.log(myMultiply(5, 2));
```
<br>

### Void Function Type

> The type `void` is a little like the opposite of `any`: the absence of having any type at all. You may commonly see this as the return type of functions that do not return a value:

```ts
  function sayHello(): void {
    console.log('Hello!');
    // return myName; // Not possible because the function can't return anything due to the void assigned type (more on this below).
  }
```

> Declaring variables of type `void` is not useful because you can only assign `undefined` or `null` to them:

```ts
  let unusable: void = undefined;
```

<br>

### Objects

> The type `object` represents the non-primitive type, i.e. any thing that is not `number`, `string`, `boolean`, `symbol`, `null`, or `undefined`.

In JavaScript, so as in TypeScript, Objects are comprised of key-value pairs. We can assign types to the `object` key-value pairs, like so:

```ts
  let userData: { name: string, age: number } = {
    name: 'Max',
    age: 27
  };
  // userData = { // Not valid
  //   name: 2,
  //   age: 'Age'
  // };
  // userData = { // Not valid
  //   a: 'Robert',
  //   b: 24
  // };
  userData = {
    name: 'Robert',
    age: 24
  };
```
<br>

#### Complex Objects

As you may expect, the assigned types to the `object` key-value pairs can reach high levels of complexity, for example:

```ts
  let complex: { data: number[], output: (all: boolean) => number[] } = {
    data: [100, 3,99, 10],
    output: function(all: boolean): number[] {
      return this.data
    }
  };
  // complex = {}; // Not possible.
```

<br>

#### Optional object properties

In TypeScript, all newly declared **object properties** (including both **function parameters**, and **interface properties**) may be declared as *optional*. To do so, we must place a `?` character after the key (or name) of the property when declaring it (a postfix notation). Here's an example:

```ts
  const right: { name: string, age?: number } = {
    name: 'Robert'
  };

  const alsoRight: { name: string, age?: number } = {
    name: 'Robert',
    age: 24
  };

  // This is not possible because the name key-value pair is missing.
  // const wrong: { name: string, age?: number } = {
  //   age: 24
  // };
```
<br>

### Alias

Writing complex and long types can quickly become dull and impractical. For a DRY approach, it's possible to create aliases for types, essentially creating your own types. Here's an example using the complex object above:

```ts
  type Complex = { data: number[], output: (all: boolean) => number[] };

  let complex2: Complex  = {
    data: [100, 3,99, 10],
    output: function(all: boolean): number[] {
      return this.data
    }
  };
```

# References
- rmolinamir typescript-cheatsheet
