# Day 4: TypeScript Fundamentals - Part 1

## Core Concepts

- TypeScript = JavaScript + Static Types
- Types catch bugs BEFORE runtime
- Type inference: TypeScript can guess types
- Explicit annotations: when you need to be specific

## Basic Types Learned

```typescript
string, number, boolean, arrays, null, undefined;
```

## Aha Moments

- В целом с темой я был знаком, поэтому ничего удивительного не нашел для себя.
- TypeScript гораздо лучше JavaScript

## Struggled With

- Немного долго понимал как работают функции в TypeScript

## Key Syntax

### Variables

```typescript
let name: string = "value";
let count: number = 42;
let items: string[] = ["a", "b"];
```

### Functions

```typescript
function greet(name: string): string {
  return `Hello, ${name}`;
}

async function getData(id: number): Promise<User> {
  // ...
}
```

### Interfaces

```typescript
interface User {
  id: number;
  name: string;
  email?: string; // Optional
}
```

## Questions for Tomorrow

- Узнать больше про составные типы `type` и `interface`

## English Terms Learned

- type annotation - аннотация типа
- type inference - вывод типа
- interface - интерфейс
- optional property - опциональное свойство
- readonly - только для чтения