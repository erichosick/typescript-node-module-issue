# typescript-node-module-issue

This package shows a difference in behavior with the [import declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) for typescript when the path of the typescript file does and does not contain a directory named `node_modules`.

## The Issue

Given a typescript file:

```typescript
// File: add.ts located in sub-folder2/node_modules2 and sub-folder/node_modules
const add = (left: number, right: number): number => {
  return left + right;
};

export default add;
```

An import as follows works because the path **does not** contain a folder named `node_modules`.

```typescript
// File: works.ts
import add from './sub-folder2/node_modules2/add';
console.log(add(1, 1));
```

However, when the path **does** contain a folder named `node_modules` then the import fails with the error `SyntaxError: Unexpected token ...`:

```typescript
// File: fails.ts
import add from './sub-folder/node_modules/add';
console.log(add(1, 1));
```

## How to repeat the behavior

```bash
# install package dependencies
$ yarn

// this works
$ yarn ts-node works

// fails with SyntaxError: Unexpected token ':'
$ yarn ts-node fails

```
