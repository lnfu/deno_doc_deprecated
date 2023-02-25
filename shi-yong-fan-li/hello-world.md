# Hello World

### 基本概念

Deno 不需要任何額外的工具和配置就可以直接執行 JavaScript 或 TypeScript 程式碼。

### 概述

Deno 是一個 JavaScript 和 TypeScript 的安全執行環境。在這個範例中，我們將會看到可以用 JavaScript 或是 TypeScript 撰寫出相同功能的程式，並在 Deno 環境中執行。

### JavaScript

下面這段 JavaScript 程式碼中，`Hello [名字]` 會輸出到螢幕，並且保證名字的首字母大寫。\
**執行指令**: `deno run hello-world.js`

```javascript
/**
 * hello-world.js
 */
function capitalize(word) {
  return word.charAt(0).toUpperCase() + word.slice(1);
}

function hello(name) {
  return "Hello " + capitalize(name);
}

console.log(hello("john"));
console.log(hello("Sarah"));
console.log(hello("kai"));

/**
 * Output:
 *
 * Hello John
 * Hello Sarah
 * Hello Kai
 */
```

### TypeScript

這段 TypeScript 程式碼和上述的 JavaScript 範例基本上是完全相同的，只是加上了 TypeScript 支援的額外型別資訊。\
要用來執行程式的指令也和 JavaScript 大致相同，只需要將副檔名 `.js` 改成 `.ts`。\
**執行指令**: `deno run hello-world.ts`

```typescript
/**
 * hello-world.ts
 */
function capitalize(word: string): string {
  return word.charAt(0).toUpperCase() + word.slice(1);
}

function hello(name: string): string {
  return "Hello " + capitalize(name);
}

console.log(hello("john"));
console.log(hello("Sarah"));
console.log(hello("kai"));

/**
 * Output:
 *
 * Hello John
 * Hello Sarah
 * Hello Kai
 */
```
