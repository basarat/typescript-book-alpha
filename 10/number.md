### `number`
JavaScript has only one number type. It is a double-precision 64-bit number. It is represented in TypeScript as the `number` data type. 

> JavaScript does not have a special runtime value for integers, so there's no `int` or `float`.

```ts
// Declare a variable of type number
let foo: number;

// Means it can hold values like:
foo = 123; 
foo = 456.798;
```

### Arithmetic Operators
Arithmetic operations (+,-,*,/,%,**) work on numbers the same as you would expect:

```ts
const foo = 3;
const bar = 5;
console.log(foo + 1); // addition: 4
console.log(foo / bar); // division: 0.6
console.log(foo * bar); // multiplication: 15
console.log(foo - bar); // subtraction: -2;
console.log(foo % 2); // remainder: 1
console.log(foo ** 2); // exponentiation: 9
```

In addition, JavaScript also has these as *assignment* operators e.g. `+=` is called *addition assignment operator*. They just expand to operator followed by assignment e.g. `x+= y` is same as `x = x + y`. 

```ts
let foo = 123;
foo += 1;
console.log(foo); // 124
```

List of assignment operators : `+=` `-=` `*=` `/=` `%=` `*=`

### Bitwise opeators 
TODO
```
<< left shift
>> right shift 
>>> unsigned right shift
 
& 
|
^
```
They also have assignment variants (e.g. `&=`)

### number limitations
Below we discuss its limitations along with a recommended solution.

#### Decimal
For those familiar with doubles / float in other languages, you would know that binary floating point numbers *do not* map correctly to Decimal numbers. A trivial (and famous) example with JavaScript's built in numbers is shown below:

```js
console.log(.1 + .2); // 0.30000000000000004
```

> For true decimal math use `big.js` mentioned below.

> When you have a base 10 system (like ours), it can only express fractions that use a prime factor of the base. The prime factors of 10 are 2 and 5. So 1/2, 1/4, 1/5, 1/8, and 1/10 can all be expressed cleanly because the denominators all use prime factors of 10. In contrast, 1/3, 1/6, and 1/7 are all repeating decimals because their denominators use a prime factor of 3 or 7. In binary (or base 2), the only prime factor is 2. So you can only express fractions cleanly which only contain 2 as a prime factor. In binary, 1/2, 1/4, 1/8 would all be expressed cleanly as decimals. While, 1/5 or 1/10 would be repeating decimals. So 0.1 and 0.2 (1/10 and 1/5) while clean decimals in a base 10 system, are repeating decimals in the base 2 system the computer is operating in. When you do math on these repeating decimals, you end up with leftovers which carry over when you convert the computer's base 2 (binary) number into a more human readable base 10 number.

#### Integer
The integer limits represented by the built in number type are `Number.MAX_SAFE_INTEGER` and `Number.MIN_SAFE_INTEGER`.

```js
console.log({max: Number.MAX_SAFE_INTEGER, min: Number.MIN_SAFE_INTEGER});
// {max: 9007199254740991, min: -9007199254740991}
```

**Safe** in this context refers to the fact that the value *cannot be the result of a rounding error*.

The unsafe values are `+1 / -1` away from these safe values and any amount of addition / subtraction will *round* the result.

```js
console.log(Number.MAX_SAFE_INTEGER + 1 === Number.MAX_SAFE_INTEGER + 2); // true!
console.log(Number.MIN_SAFE_INTEGER - 1 === Number.MIN_SAFE_INTEGER - 2); // true!

console.log(Number.MAX_SAFE_INTEGER);      // 9007199254740991
console.log(Number.MAX_SAFE_INTEGER + 1);  // 9007199254740992 - Correct
console.log(Number.MAX_SAFE_INTEGER + 2);  // 9007199254740992 - Rounded!
console.log(Number.MAX_SAFE_INTEGER + 3);  // 9007199254740994 - Rounded - correct by luck
console.log(Number.MAX_SAFE_INTEGER + 4);  // 9007199254740996 - Rounded!
```

To check safety you can use ES6 `Number.isSafeInteger`:

```js
// Safe value
console.log(Number.isSafeInteger(Number.MAX_SAFE_INTEGER)); // true

// Unsafe value
console.log(Number.isSafeInteger(Number.MAX_SAFE_INTEGER + 1)); // false

// Because it might have been rounded to it due to overflow
console.log(Number.isSafeInteger(Number.MAX_SAFE_INTEGER + 10)); // false
```

> JavaScript will eventually get [BigInt](https://developers.google.com/web/updates/2018/05/bigint) support. For now, if you want arbitrary precision integer math use `big.js` mentioned below.

#### big.js
Whenever you use math for financial calculations (e.g. GST calculation, money with cents, addition etc) use a library like [big.js](https://github.com/MikeMcl/big.js/) which is designed for
* Perfect decimal math
* Safe out of bound integer values

Installation is simple:
```bash
npm install big.js @types/big.js
```

Quick Usage example:

```js
import { Big } from 'big.js';

export const foo = new Big('111.11111111111111111111');
export const bar = foo.plus(new Big('0.00000000000000000001'));

// To get a number:
const x: number = Number(bar.toString()); // Loses the precision
```

> Do not use this library for math used for UI / performance intensive purposes e.g charts, canvas drawing etc.

#### NaN
When some number calculation is not representable by a valid number, JavaScript returns a special `NaN` value. A  classic example is imaginary numbers:

```js
console.log(Math.sqrt(-1)); // NaN
```

Note: Equality checks **don't** work on `NaN` values. Use `Number.isNaN` instead:

```js
// Don't do this
console.log(NaN === NaN); // false!!

// Do this
console.log(Number.isNaN(NaN)); // true
```

#### Infinity
The outer bounds of values representable in Number are available as static `Number.MAX_VALUE` and `-Number.MAX_VALUE` values.

```js
console.log(Number.MAX_VALUE);  // 1.7976931348623157e+308
console.log(-Number.MAX_VALUE); // -1.7976931348623157e+308
```

Values outside the range where precision isn't changed are clamped to these limits e.g.

```js
console.log(Number.MAX_VALUE + 1 == Number.MAX_VALUE);   // true!
console.log(-Number.MAX_VALUE - 1 == -Number.MAX_VALUE); // true!
```

Values outside the range where precision is changed resolve to special values `Infinity`/`-Infinity` e.g.

```js
console.log(Number.MAX_VALUE + 10**1000);  // Infinity
console.log(-Number.MAX_VALUE - 10**1000); // -Infinity
```

Of-course, these special infinity values also show up with arithmetic that requires it e.g.

```js
console.log( 1 / 0); // Infinity
console.log(-1 / 0); // -Infinity
```

You can use these `Infinity` values manually or using static members of the `Number` class as shown below:

```js
console.log(Number.POSITIVE_INFINITY === Infinity);  // true
console.log(Number.NEGATIVE_INFINITY === -Infinity); // true
```

Fortunately comparison operators (`<` / `>`) work reliably on infinity values:

```js
console.log( Infinity >  1); // true
console.log(-Infinity < -1); // true
```

#### Infinitesimal

The smallest non-zero value representable in Number is available as static `Number.MIN_VALUE`

```js
console.log(Number.MIN_VALUE);  // 5e-324
```

Values smaller than `MIN_VALUE` ("underflow values") are converted to 0.

```js
console.log(Number.MIN_VALUE / 10);  // 0
```

> Further intuition: Just like values bigger than `Number.MAX_VALUE` get clamped to INFINITY, values smaller than `Number.MIN_VALUE` get clamped to `0`.
