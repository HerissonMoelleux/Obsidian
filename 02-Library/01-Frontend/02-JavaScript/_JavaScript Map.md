# JavaScript Map

> Язык веба. Без глубокого понимания JS — React будет магией.

---

## 🎯 Почему эта папка существует?

JavaScript — **язык React**. Многие "React-проблемы" на самом деле — непонимание JS:
- Почему `this` не работает в callback? → JS вопрос
- Почему state не обновляется сразу? → Closures + async
- Как работает `map`, `filter`? → JS fundamentals

**Аналогия:** Нельзя хорошо писать на React, не понимая JS. Это как пытаться писать стихи, не зная грамматики.

---

## 📁 Structure

```
02-JavaScript/
├── Core/
│   ├── Types.md                  # Primitives vs Objects, typeof
│   ├── Type Coercion.md          # == vs ===, implicit conversion
│   ├── Variables.md              # var, let, const, hoisting, TDZ
│   └── Operators.md              # Spread, rest, ?., ??
│
├── Functions/
│   ├── Function Types.md         # Declaration vs Expression vs Arrow
│   ├── Closures.md               # ⭐ Критически важно!
│   ├── Scope.md                  # Global, function, block scope
│   ├── this Keyword.md           # ⭐ Частый вопрос на собесах
│   └── Higher-Order Functions.md # map, filter, reduce, callbacks
│
├── Objects/
│   ├── Object Basics.md          # Creation, properties, methods
│   ├── Prototypes.md             # Прототипное наследование
│   ├── Classes.md                # ES6 classes, syntactic sugar
│   └── Destructuring.md          # Objects & arrays destructuring
│
├── Async/
│   ├── Event Loop.md             # ⭐ Must know для собесов
│   ├── Callbacks.md              # Callback hell, why promises
│   ├── Promises.md               # Creation, chaining, Promise.all
│   └── Async-Await.md            # Syntax, error handling
│
├── Modules/
│   └── ES Modules.md             # import, export, dynamic imports
│
└── Modern Features/
    └── ES6+ Features.md          # Template literals, optional chaining, etc.
```

---

## 🧱 Core

Базовые строительные блоки языка.

### Topics

- [[Types]] — примитивы vs объекты, typeof, instanceof
- [[Coercion]] — неявное преобразование типов (`==`vs`===`)
- [[Variables]] — var, let, const, hoisting, TDZ
- [[Operators]] — spread, rest, optional chaining, nullish coalescing
- [[Control Flow]] — if, switch, loops, iteration protocols

### Key Questions (Interview)

- Разница между `==` и `===`?
- Что такое hoisting?
- `null` vs `undefined`?

---

## ⚙️ Functions

Функции — основа всего в JS.

### Topics

- [[Function Declarations vs Expressions]]
- [[Arrow Functions]] — синтаксис, отличия, когда использовать
- [[Closures]] — замыкания, лексическое окружение
- [[Scope]] — глобальный, функциональный, блочный
- [[this Keyword]] — контекст вызова, bind, call, apply
- [[Higher-Order Functions]] — map, filter, reduce, callbacks

### Key Questions (Interview)

- Что такое замыкание? Приведи пример.
- Как работает `this` в стрелочных функциях?
- Разница между `call`, `apply`, `bind`?

### 💡 Deep Dive
```javascript
// Classic closure example
function createCounter() {
  let count = 0;
  return {
    increment: () => ++count,
    getCount: () => count
  };
}
```

---

## 🏗️ Objects

Объектная модель JavaScript.

### Topics

- [[Object Basics]] — создание, свойства, методы
- [[Prototypes]] — прототипное наследование, __proto__, prototype
- [[Classes]] — ES6 синтаксис, syntactic sugar над прототипами
- [[Destructuring]] — объектов и массивов
- [[Object Methods]] — Object.keys, values, entries, assign, freeze

### Key Questions (Interview)

- Как работает прототипное наследование?
- Разница между class и function constructor?
- Как сделать immutable объект?

---

## ⏳ Async

Асинхронность — то, что отличает JS от других языков.

### Topics

- [[Event Loop]] — call stack, task queue, microtasks
- [[Callbacks]] — callback hell, почему это проблема
- [[Promises]] — создание, chaining, Promise.all, Promise.race
- [[Async-Await]] — синтаксический сахар, error handling
- [[Error Handling]] — try-catch в async коде

### Key Questions (Interview)

- Объясни Event Loop простыми словами
- Разница между microtasks и macrotasks?
- Как обработать ошибки в async/await?

---

## 📦 Modules

Организация кода в модули.

### Topics

- [[ES Modules]] — import, export, default export
- [[Module Patterns]] — named exports vs default
- [[Dynamic Imports]] — import() для code splitting

### Key Questions (Interview)

- Разница между named и default export?
- Что такое tree shaking?

---

## ✨ Modern Features

ES6+ фичи, которые нужно знать.

### Topics

- [[Template Literals]] — интерполяция, tagged templates
- [[Optional Chaining]] — `?.` оператор
- [[Nullish Coalescing]] — `??` оператор
- [[Spread and Rest]] — `...` в разных контекстах
- [[Array Methods]] — flat, flatMap, at, findLast

---

## 🔗 Connections

- [[_TypeScript Map]] — TS расширяет JS типами
- [[_React Map]] — React = JS + JSX
- [[_Web Concepts Map]] — JS работает в браузере

---

## 📈 Progress

### Must Know (Junior)
- [ ] Closures & Scope
- [ ] this keyword
- [ ] Promises & async/await
- [ ] Event Loop basics
- [ ] ES6+ features

### Good to Know (Junior+)
- [ ] Prototypes deep dive
- [ ] Microtasks vs Macrotasks
- [ ] Generators & Iterators

---

*Part of [[_Frontend Development Map]]*
