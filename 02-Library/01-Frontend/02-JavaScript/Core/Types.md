# Types

> Primitives vs Objects — фундаментальное разделение в JavaScript.

---

## Primitive Types

### Какие примитивы существуют?
<!-- string, number, boolean, null, undefined, symbol, bigint -->

### Почему они называются "примитивы"?
<!-- immutable, stored by value, no methods (но autoboxing!) -->

### Autoboxing — как примитивы имеют методы?
<!-- "hello".toUpperCase() — как это работает? -->

---

## Objects

### Что является объектом в JS?
<!-- arrays, functions, dates, objects, etc. -->

### Reference vs Value — в чём разница?
<!-- почему изменение объекта меняет "оригинал" -->

### Как проверить равенство объектов?
<!-- {} === {} → false, почему? -->

---

## typeof Operator

### Таблица результатов typeof
<!-- заполни таблицу для всех типов -->

| Value | typeof result |
|-------|---------------|
| `"hello"` | |
| `42` | |
| `true` | |
| `null` | |
| `undefined` | |
| `{}` | |
| `[]` | |
| `function(){}` | |
| `Symbol()` | |

### typeof null === "object" — почему?
<!-- исторический баг JS -->

---

## Проверка типов

### typeof vs instanceof — когда что?
<!-- typeof для примитивов, instanceof для объектов -->

### Array.isArray() — зачем отдельный метод?
<!-- typeof [] === "object", нужен способ отличить -->

### Object.prototype.toString.call() — надёжный способ
<!-- "[object Array]", "[object Date]", etc. -->

---

## Gotchas

### NaN — странности
<!-- typeof NaN, NaN === NaN, Number.isNaN() -->

### Falsy values — полный список
<!-- 0, "", null, undefined, NaN, false -->

---

## Interview Questions

- Сколько примитивных типов в JavaScript?
- Почему `typeof null === "object"`?
- Как проверить, что переменная — массив?
- Что такое autoboxing?
