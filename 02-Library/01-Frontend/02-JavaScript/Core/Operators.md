# Operators

> Spread, Rest, Optional Chaining, Nullish Coalescing — современный JS синтаксис.

---

## Spread Operator (...)

### В массивах

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// Копирование массива
const copy = // ???

// Объединение массивов
const merged = // ???

// Добавление элементов
const withExtra = // ???
```

### В объектах

```javascript
const user = { name: 'John', age: 30 };

// Копирование объекта
const copy = // ???

// Слияние объектов (какой порядок важен?)
const updated = { ...user, age: 31 }; // ???
const wrong = { age: 31, ...user };   // ???
```

### В аргументах функции

```javascript
const numbers = [1, 2, 3, 4, 5];
Math.max(...numbers); // ???

// Как это работало до spread?
Math.max.apply(null, numbers);
```

### Shallow Copy предупреждение
<!-- spread копирует только первый уровень -->

```javascript
const nested = { a: { b: 1 } };
const copy = { ...nested };
copy.a.b = 2;
console.log(nested.a.b); // ???
```

---

## Rest Operator (...)

### В параметрах функции

```javascript
function sum(...numbers) {
  // numbers это ???
  return numbers.reduce((a, b) => a + b, 0);
}

sum(1, 2, 3, 4); // ???
```

### Отличие от arguments
<!-- rest это настоящий массив, arguments — нет -->

### В деструктуризации

```javascript
const [first, second, ...rest] = [1, 2, 3, 4, 5];
// first = ???
// second = ???
// rest = ???

const { name, ...otherProps } = { name: 'John', age: 30, city: 'NYC' };
// name = ???
// otherProps = ???
```

### Где может быть rest?
<!-- только последним элементом -->

---

## Spread vs Rest — как отличить?

### Правило
<!-- spread "разворачивает", rest "собирает" -->

```javascript
// Это spread или rest?
const arr = [...items];           // ???
function fn(...args) {}           // ???
console.log(...arr);              // ???
const [a, ...rest] = arr;         // ???
```

---

## Optional Chaining (?.)

### Зачем нужен?
<!-- безопасный доступ к вложенным свойствам -->

### До optional chaining

```javascript
// Старый способ
const city = user && user.address && user.address.city;

// Или
const city = user?.address?.city; // ???
```

### С методами

```javascript
const result = obj.method?.(); // ???
// Что если method не существует?
// Что если method существует но не функция?
```

### С массивами

```javascript
const first = arr?.[0]; // ???
```

### С delete

```javascript
delete user?.address; // ???
```

### Short-circuit — важно понимать

```javascript
const x = null;
x?.a.b.c; // Что произойдёт?
```

---

## Nullish Coalescing (??)

### Зачем нужен?
<!-- дефолтное значение только для null/undefined -->

### Отличие от ||

```javascript
const value1 = 0 || 'default';    // ???
const value2 = 0 ?? 'default';    // ???

const value3 = '' || 'default';   // ???
const value4 = '' ?? 'default';   // ???

const value5 = false || 'default'; // ???
const value6 = false ?? 'default'; // ???
```

### Когда использовать || vs ??

| Случай | Используй |
|--------|-----------|
| Любое falsy = default | `\|\|` |
| Только null/undefined = default | `??` |

### Нельзя смешивать с && и || без скобок

```javascript
// SyntaxError
const x = a || b ?? c;

// Нужно явно указать приоритет
const x = (a || b) ?? c;
const x = a || (b ?? c);
```

---

## Комбинации

### Optional Chaining + Nullish Coalescing

```javascript
const city = user?.address?.city ?? 'Unknown';
// Что это делает?
```

### Практический пример

```javascript
// API response может быть неполным
const displayName = response?.data?.user?.name ?? 'Anonymous';
const avatar = response?.data?.user?.avatar ?? '/default-avatar.png';
```

---

## Logical Assignment Operators (ES2021)

### ||= (OR assignment)

```javascript
let x = null;
x ||= 'default'; // x = ???

let y = 'value';
y ||= 'default'; // y = ???
```

### &&= (AND assignment)

```javascript
let x = 'value';
x &&= 'new value'; // x = ???

let y = null;
y &&= 'new value'; // y = ???
```

### ??= (Nullish assignment)

```javascript
let x = null;
x ??= 'default'; // x = ???

let y = 0;
y ??= 'default'; // y = ???
```

---

## Gotchas

### Spread не клонирует глубоко
<!-- nested objects всё ещё по reference -->

### Optional chaining возвращает undefined, не null
<!-- даже если изначальное значение было null -->

### ?? имеет низкий приоритет
<!-- используй скобки для ясности -->

---

## Interview Questions

- В чём разница между spread и rest?
- Чем `??` отличается от `||`?
- Что вернёт `user?.address?.city` если user = null?
- Как сделать deep copy объекта? (spread не работает)
- Что такое short-circuit evaluation в optional chaining?

---
#javascript #core #operators #es6
