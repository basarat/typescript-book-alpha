
You can wrap your `case` bodies in `{}` to reuse variable names reliably in different `case` statement as shown below:

```ts
switch (name) {
    case 'x': {
        const x = 5;
        // ...
        break;
    }
    case 'y': {
        const x = 10;
        // ...
        break;
    }
}
```
