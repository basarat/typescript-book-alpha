### `let`

If you want to reassign a variable you can use `let` (instead of `const`). Here is an example where we keep a running current `minimum`:  

```ts 
/**
 * Find the min in an array of numbers
 */
export function min(array: number[]): number {
  let minimum = Infinity; // Declared with `let`
  for (const item of array) {
    if (item < minimum) {
      minimum = item;  // Because we are going to reassign it
    }
  }
  return minimum;
}
```

#### Creating without assigment
Since `let` allows you to do reassignment you can create it without doing an assignment e.g. 

```ts
let foo: number;

// Later do some assignment
```

If you are not going to do an assignment immediately, you should add a type annotation (in our example we added `: number`). Otherwise, TypeScript will infer `any` which is very unsafe type we will talk about later.

#### Similarity with const
Other than the assignment/reassignment difference, `const` and `let` are mostly the same. Here are a few facts about `let/const` worth mentioning again: 

* They are block scoped.
