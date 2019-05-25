## Why TypeScript

If you are reading this book, hopefully you don't need too much convincing yourself. However, if you need to convince a mate of yours, here's a quick list of reasons.

### You already have types
A wise friend once said: 

> All programs are just data and code that operates on data

TypeScript provides you and opportunity to describe the `data` portion of your `data + code`. 

### JavaScript is TypeScript 
There were (and will continue to be) a lot of competitors in `Some syntax to JavaScript` compilers. TypeScript is different from them in that `Your JavaScript is TypeScript`. Here's a diagram:


![JavaScript is TypeScript](https://raw.githubusercontent.com/basarat/typescript-alpha-book/master/images/javascript-is-typescript.png)

TypeScript is just JavaScript with types to help.

### Catching JavaScript Errors 

I have a saying, "TypeScript is like Anders doing a code review for your JavaScript". TypeScript will try to protect you from portions of JavaScript that never worked (so you don't need to remember this stuff):

```ts
[] + []; // JavaScript will give you "" (which makes little sense), TypeScript will error

//
// other things that are nonsensical in JavaScript
// - don't give a runtime error (making debugging hard)
// - but TypeScript will give a compile time error (making debugging unnecessary)
//
{} + []; // JS : 0, TS Error
[] + {}; // JS : "[object Object]", TS Error
{} + {}; // JS : NaN or [object Object][object Object] depending upon browser, TS Error
"hello" - 1; // JS : NaN, TS Error

function add(a,b) {
  return
    a + b; // JS : undefined, TS Error 'unreachable code detected'
}
```

* TODO: https://basarat.gitbooks.io/typescript/content/docs/getting-started.html
* TODO: https://basarat.gitbooks.io/typescript/content/docs/why-typescript.html types can be explicit, inferred and are structural, type errors do not prevent emit, ambient types. 
