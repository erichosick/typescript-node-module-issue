# typescript-node-module-issue

This package shows a difference in behavior with the [import declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) for typescript when the path of the typescript file does and does not contain a directory named `node_modules`.

## Resolution

Keeping this repository here for posterity. See [issuecomment](https://github.com/nodejs/node/issues/45453#issuecomment-1313121137) and [expected behavior](https://github.com/TypeStrong/ts-node/blob/ba950599c6bfcba32b514b33d254094b278b744e/website/docs/scope.md#skipping-node_modules).

The solution is to run:

```bash
yarn ts-node --skipIgnore fails
```

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
