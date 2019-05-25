### `const`
`const` allows you to create a variable that can never be re-assigned. Here is an example that defines a variable using `const`: 

```ts
const foo = 123;
```

Since `const` prevents reassignment, the following will be pointed out as an error by TypeScript: 

```ts
const foo = 123;
foo = 456; // TS Error : Cannot assign to `foo` because it is a constant
```

#### Use case: Magic Literals
`const` is a good practice for both readability and maintainability and avoids using *magic literals* e.g.

```ts
// Low readability
if (x > 10) {
}

// Better!
const maxRows = 10;
if (x > maxRows) {
}
```

#### const declarations must be initialized
The following is a compiler error:

```ts
const foo; // ERROR: const declarations must be initialized
```

Makes sense as you cannot assign later :).

#### Block scoped

A block is something delimited by parethesis `{ /* in a block */ }`. `const` variables are block scoped. That means they only exist in the block that they are defined. e.g.: 

```ts
{ 
  const foo = 123;
  console.log(foo); // Okay 
}
console.log(foo); // TS Error: cannot find name `foo`
```

Blocks are created by common control flow constructs like `if`/`else`/`while` etc: 

```ts
const foo = 123;
if (true) {
  const foo = 456; // A new variable limited to this `if` block
}
```

#### Avoid explicitly annotating a const
You normally don't need to add a type annotation (e.g. don't do `const foo: number = 123`) to a `const` as TypeScript will automatically infer the most strict version it can e.g. 

```ts
const foo = 123; // TypeScript infers foo:123

if (foo === 456) { // TS Error: types `123` and `456` have no overlap

}
```

