## The nature of the TypeScript Type System

Type systems come in various flavours. There are choices that the TypeScript team has made when designing the langauge that we will cover here. 

### Types can be implicit

> types have a way of being unnecessarily ceremonious. TypeScript is very particular about keeping the barrier to entry as low as possible.

TypeScript will try to infer as much of the type information as it can in order to give you type safety with minimal cost of productivity during code development. For example, in the following example TypeScript will know that foo is of type `number` below and will give an error on the second line as shown:

```ts
let foo = 123;
foo = '456'; // Error: cannot assign `string` to `number`

// Is foo a number or a string?
```
This type inference is well motivated. If you do stuff like shown in this example, then, in the rest of your code, you cannot be certain that `foo` is a `number` or a `string`. Such issues turn up often in large multi-file code bases. We will deep dive into the type inference rules later.


* TODO: https://basarat.gitbooks.io/typescript/content/docs/why-typescript.html types can be explicit, inferred and are structural, type errors do not prevent emit, ambient types. 
