## TypeScriptのインターセクション型 (Intersection Type, &) は文字通り複数の型を組み合わせて一つの型を作る機能です。

## 1. 基本文法

```typescript
type A = { name: string };
type B = { age: number };

type Person = A & B;

const p: Person = {
  name: "Kim",
  age: 30,
};
```
- A & B → A と B の両方を満たす必要がある。
- 結果的に Person は { name: string; age: number } 型になる。

## 2. インターセクションの特徴

### (1) 和集合ではなく交差 (AND)

- | (Union) はどちらか一方が可能。
- & (Intersection) は両方を持たなければならない。

```typescript
type Cat = { meow: () => void };
type Dog = { bark: () => void };

type CatDog = Cat & Dog;

const hybrid: CatDog = {
  meow: () => console.log("nya-"),
  bark: () => console.log("wan!"),
};
```
CatDog は猫+犬の両方の性質を持つ型。

### (2) プロパティが競合する時

```typescript
type X = { value: string };
type Y = { value: number };

type Z = X & Y; // { value: string & number }

```
- string & number は存在できない型 → never。
- つまり Z 型は実質的に使用不可能。

### (3) ユニオンと混ぜて使用

```typescript
type A = { name: string };
type B = { age: number };

type AB = A & { role: "admin" | "user" };

const u: AB = {
  name: "Lee",
  role: "admin", // "user"も可能
};
```
