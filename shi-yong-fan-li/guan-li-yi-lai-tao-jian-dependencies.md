# 管理依賴套件（dependencies）

### 基本概念

* Deno 使用 URL 來管理依賴套件
* 習慣上會將所有依賴的 URL 放到本機的 `deps.ts` 檔案。再把要使用的函式導出到本地模組中。
* 另外，開發者專用的套件通常會放在 `dev_deps.ts` 檔案。
* 詳細資訊請參閱[模組](../ji-chu/mo-zu-modules.md)

### 概述

Deno 並沒有一個套件管理員來負責匯入本地模組需要的外部模組。

{% hint style="info" %}
Node.js 有 npm 這個軟體套件管理系統負責管理。
{% endhint %}

那要如何管理遠端的依賴套件呢？在大型專案中，若是我們將所有依賴的套件都個別匯入成單獨的模組將會非常麻煩且需要耗費大量時間在套件的更新上。

在 Deno 中，最簡單解決這個問題的方式是建立一個 `deps.ts` 檔案，所有需要的遠端依賴套件將會在這個檔案中被引用，並且重新導出需要的方法（method）和類別（class）。本地模組可以透過引用 `dep.ts` 檔案獲得這些遠端依賴套件。

<mark style="color:red;">未完成</mark>

### 範例

```typescript
/**
 * deps.ts
 *
 * This module re-exports the required methods from the dependant remote Ramda module.
 */
export {
  add,
  multiply,
} from "https://x.nest.land/ramda@0.27.0/source/index.js"
```

<mark style="color:red;">未完成</mark>
