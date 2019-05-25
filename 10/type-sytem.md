## The nature of the TypeScript Type System

Type systems come in various flavours. There are choices that the TypeScript team has made when designing the langauge that we will cover here. 

### Type inference

> types have a way of being unnecessarily ceremonious. TypeScript is very particular about keeping the barrier to entry as low as possible.

TypeScript will try to infer as much of the type information as it can in order to give you type safety with minimal cost of productivity during code development. For example, in the following example TypeScript will know that foo is of type `number` below and will give an error on the second line as shown:

```ts
let foo = 123;
foo = '456'; // Error: cannot assign `string` to `number`

// Is foo a number or a string?
```
This type inference is well motivated. If you do stuff like shown in this example, then, in the rest of your code, you cannot be certain that `foo` is a `number` or a `string`. Such issues turn up often in large multi-file code bases. We will deep dive into the type inference rules later.

### Structural typing

In some languages (specifically nominally typed ones) static typing results in unnecessary ceremony because even though *you know* that the code will work fine the language semantics force you to copy stuff around. This is why stuff like [automapper for C#](http://automapper.org/) is *vital* for C#. 

In TypeScript because we really want it to be easy for JavaScript developers with a minimum cognitive overload, types are *structural*. This means that *duck typing* is a first class language construct. Consider the following example. The function `iTakePoint2D` will accept anything that contains all the things (`x` and `y`) it expects:

```ts
interface Point2D {
    x: number;
    y: number;
}
interface Point3D {
    x: number;
    y: number;
    z: number;
}
let point2D: Point2D = { x: 0, y: 10 }
let point3D: Point3D = { x: 0, y: 10, z: 20 }
function iTakePoint2D(point: Point2D) { /* do something */ }

iTakePoint2D(point2D); // exact match okay
iTakePoint2D(point3D); // extra information okay
iTakePoint2D({ x: 0 }); // Error: missing information `y`
```

### Type errors do not prevent JavaScript emit
To make it easy for you to migrate your JavaScript code to TypeScript, even if there are compilation errors, by default TypeScript *will emit valid JavaScript* the best that it can. e.g.

```ts
let foo = 123;
foo = '456'; // Error: cannot assign a `string` to a `number`
```

will emit the following js:

```ts
let foo = 123;
foo = '456';
```

So you can incrementally upgrade your JavaScript code to TypeScript.

> If you don't want to emit any JavaScript if there is a TypeScript error there is a typescript option that you can set `'noEmitOnError' : true`.

* TODO: https://basarat.gitbooks.io/typescript/content/docs/why-typescript.html types can be explicit, inferred and are structural, type errors do not prevent emit, ambient types. 
