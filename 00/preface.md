# Preface 

A few years ago (at this point 4) I wrote the original [TypeScript Deep Dive](https://github.com/basarat/typescript-book/). It was geared at the audience that TypeScript needed to capture at that time. They were JavaScript engineers that needed some form to tooling to help them scale their increasingly large codebases. TypeScript was exactly that tool, at that book fills that gap. 

However times have changed. The is a large influx of new JavaScript developers (just new to *JavaScript*) that understand (themselves or by recommendation) the value of a compile time type system for documentation and maintainability. They have the challenge of learning *both* JavaScript *and* TypeScript. This book aims to be that resource. 

## Learn JavaScript and TypeScript *at the same time*
Mastering any programming language is a cyclic problem. There are some fundamentals that are inherantly interdependent. It is much more significant when you try to isolate TypeScript additions while trying to also teach JavaScript.  

Lets consider a simple example of explaining the significant `in` operator in JavaScript and how it TypeScript understands its impact on type analysis: 

```ts
interface A {
  x: number;
}
interface B {
  y: string;
}

function doStuff(q: A | B) {
  if ('x' in q) {
    // TypeScript will infer `q: A` in this block
  }
  else {
    // TypeScript will infer `q: V` in this block
  }
}
```

In order to understand this example you need to be aware of a few type concetps like *type definitions* (`interface`), *type annotations* (`: A | B`), *type unions* (the `|` in `A |B`) and the JavaScript implications of the `in` operator. In this case the ideal approach would be to present the `in` operator (a JavaScript concept) only after presenting type unions (a TypeScript concept). A TypeScript first approach. 

But a TypeScript first approach is not something that is plausible, even a simple code example like: 

```ts
let something: number = 123; 
```

You clearly should ideally explain *let* before you explain `:number`. A JavaScript first approach. 

The way I tried to approach it with TypeScript deep dive was present *just a little bit* of TypeScript and then lots of JavaScript followed by deep dive into TypeScript. It made sense for someone who wasn't entirely convinced about TypeScript. Presenting JavaScript in ioslation in a TypeScript context was my attempt at building confidence into the reader  learing TypeScript was worth it, because after all they were really learning JavaScript, and you *always bet on JavaScript*.

But now, I would rather write a definitive book on TypeScript without trying to sway the reader in a particular direction. Good practices and ideas will ofcourse be encouraged, but the objective will be to teach *TypeScript + JavaScript* only seperating the two when it makes it easy to grasp the idea, but otherwise not worrying about it.  

## TypeScript - The emitter
Right before TypeScript came out, JavaScript *the language* was fairly stagnant. Then TypeScript happened, next Babel / ES6 happened. One of the challenges of teaching TypeScript at that point was the fact that ideally you had to teach even existing JavaScript developers ES6, and then you also had to explain how the TypeScript you wrote would get converted to JavaScript as you often had to debug the generated JavaScript.

This is vastly no longer the case. I rarely see developers around me being aware of `__proto__` and even when they do observe the generated JavaScript, the desire to learn these mundane details is not something that seems to inspire them. 

So, I will leave them out to give you the best value for your time. They might be covered later as an appendix (as they are good to know) but they will not be the part of the main flow of the book.

## TypeScript the language service
Early on in the TypeScript ecosystem, I was doing a lot of work on TypeScript tooling as well (with atom-typescript and later alm tools) as the only official supported implementation was the windows on VSCode of the time.

So it made sense for me to add whatever I was learning, and sharing it in the book. However the compiler internals have moved on since then. They are still vaslty the same (there is still a file called `checker.ts`, there is still a `binder`, symbols still mean what they used to mean). However the internal and external apis are probably changed (if even slightly). 

TypeScript team is amazing. They released VSCode and it took the IDE environment by storm. I do author a plugin for VSCode, just for my own way of working and experimentation, called [TypeScript God](https://marketplace.visualstudio.com/items?itemName=basarat.god) but its not something that you really need. I am no longer heavily involved with maintaining public examples of TypeScript tooling as VSCode does that perfectly ❤️

So, as I've left the compiler / language service ecosystem (at least taking a break), I am not going to cover them here, as I plan to keep this guide much more easy to keep up to date compared to the previous attempt. 

## Why not TypeScript deep dive 2nd Edition 
I could definitely call this book that. However there are a few reasons for not doing it that way: 

* Don't break the internet: TypeScript deep dive is very popular. Lots of the public internet (including stackoverflow) and private internet links to it. I'd rahter not break those links.
* Creating a second edition that's vastly different (a different approach to teaching TypeScript as I've called it), is just poor expectation managment. 

So here you have it, a new book. Hope it makes your life easier 🌹
