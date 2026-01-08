# Control Flow

> Управление потоком выполнения — как программа принимает решения и повторяет действия.

---

## Условные операторы

### if / else if / else

Базовая конструкция для ветвления логики:

```javascript
const age = 18;

if (age < 13) {
  console.log('Child');
} else if (age < 20) {
  console.log('Teenager');
} else {
  console.log('Adult');
}
```

### Truthy и Falsy в условиях

`if` проверяет truthy/falsy, не строго `true`/`false`:

```javascript
// Falsy values (6 штук):
if (false) {}
if (0) {}
if ('') {}
if (null) {}
if (undefined) {}
if (NaN) {}

// Всё остальное — truthy:
if ('0') {}      // truthy! (непустая строка)
if ([]) {}       // truthy! (пустой массив)
if ({}) {}       // truthy! (пустой объект)
if (-1) {}       // truthy! (любое число кроме 0)
```

### Короткая запись (без фигурных скобок)

```javascript
// Можно, но не рекомендуется:
if (condition) doSomething();

// Лучше всегда использовать скобки для читаемости:
if (condition) {
  doSomething();
}
```

---

## Тернарный оператор

Краткая форма `if/else` для присваивания:

```javascript
// Вместо:
let status;
if (user.isAdmin) {
  status = 'admin';
} else {
  status = 'user';
}

// Используй:
const status = user.isAdmin ? 'admin' : 'user';
```

### Вложенные тернарники

```javascript
// Можно, но читаемость страдает:
const role = user.isAdmin ? 'admin' : user.isModerator ? 'moderator' : 'user';

// Лучше отформатировать:
const role = user.isAdmin 
  ? 'admin' 
  : user.isModerator 
    ? 'moderator' 
    : 'user';

// Или использовать if/else для сложных случаев
```

### Когда использовать тернарник?

- ✅ Простое присваивание одного из двух значений
- ✅ Внутри JSX (React)
- ❌ Сложная логика с side effects
- ❌ Больше двух вложенных условий

---

## switch

Альтернатива множественным `if/else if`:

```javascript
const day = 'Monday';

switch (day) {
  case 'Monday':
  case 'Tuesday':
  case 'Wednesday':
  case 'Thursday':
  case 'Friday':
    console.log('Weekday');
    break;
  case 'Saturday':
  case 'Sunday':
    console.log('Weekend');
    break;
  default:
    console.log('Invalid day');
}
```

### Важно: break!

Без `break` выполнение "проваливается" в следующий case:

```javascript
const num = 1;

switch (num) {
  case 1:
    console.log('One');
    // забыли break!
  case 2:
    console.log('Two');
    break;
}
// Output: 'One', 'Two' — оба!
```

### switch использует строгое сравнение (`===`)

```javascript
const value = '1';

switch (value) {
  case 1:
    console.log('Number one');
    break;
  case '1':
    console.log('String one');
    break;
}
// Output: 'String one'
```

### Альтернатива: Object lookup

Часто чище, чем switch:

```javascript
// Вместо switch:
const dayNames = {
  0: 'Sunday',
  1: 'Monday',
  2: 'Tuesday',
  // ...
};

const name = dayNames[new Date().getDay()] ?? 'Unknown';
```

---

## Циклы

### for

Классический цикл с счётчиком:

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);  // 0, 1, 2, 3, 4
}

// Части цикла:
// for (инициализация; условие; шаг)
```

### while

Цикл с предусловием:

```javascript
let count = 0;

while (count < 5) {
  console.log(count);
  count++;
}
```

### do...while

Цикл с постусловием — выполнится минимум один раз:

```javascript
let count = 0;

do {
  console.log(count);
  count++;
} while (count < 5);

// Выполнится даже если условие сразу false:
let x = 10;
do {
  console.log(x);  // 10 — выполнится один раз
} while (x < 5);
```

---

## Итерация по коллекциям

### for...of (ES6)

Итерация по **значениям** итерируемых объектов (массивы, строки, Map, Set):

```javascript
const fruits = ['apple', 'banana', 'cherry'];

for (const fruit of fruits) {
  console.log(fruit);  // 'apple', 'banana', 'cherry'
}

// Со строками:
for (const char of 'Hello') {
  console.log(char);  // 'H', 'e', 'l', 'l', 'o'
}

// С Map:
const map = new Map([['a', 1], ['b', 2]]);
for (const [key, value] of map) {
  console.log(key, value);  // 'a' 1, 'b' 2
}
```

### for...in

Итерация по **ключам** (свойствам) объекта:

```javascript
const user = { name: 'John', age: 30, city: 'NYC' };

for (const key in user) {
  console.log(key, user[key]);
  // 'name' 'John'
  // 'age' 30
  // 'city' 'NYC'
}
```

### for...of vs for...in

|              | for...of                               | for...in            |
| ------------ | -------------------------------------- | ------------------- |
| Итерирует по | Значениям                              | Ключам/индексам     |
| Работает с   | Итерируемыми (Array, String, Map, Set) | Любыми объектами    |
| Для массивов | ✅ Рекомендуется                        | ⚠️ Не рекомендуется |
| Для объектов | ❌ Не работает                          | ✅ Рекомендуется     |

```javascript
const arr = ['a', 'b', 'c'];

// for...of — получаем значения:
for (const value of arr) {
  console.log(value);  // 'a', 'b', 'c'
}

// for...in — получаем индексы (как строки!):
for (const index in arr) {
  console.log(index);  // '0', '1', '2'
}
```

### Почему for...in плох для массивов?

```javascript
const arr = ['a', 'b', 'c'];
arr.customProp = 'oops';

for (const key in arr) {
  console.log(key);  // '0', '1', '2', 'customProp' — включает свойства!
}

for (const value of arr) {
  console.log(value);  // 'a', 'b', 'c' — только элементы
}
```

---

## Методы массивов (функциональный подход)

Часто лучше циклов:

### forEach

```javascript
const nums = [1, 2, 3];

nums.forEach((num, index) => {
  console.log(index, num);
});

// Нельзя прервать forEach! (break не работает)
```

### map

Трансформация массива:

```javascript
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2);  // [2, 4, 6]
```

### filter

Фильтрация массива:

```javascript
const nums = [1, 2, 3, 4, 5];
const even = nums.filter(n => n % 2 === 0);  // [2, 4]
```

### reduce

Сведение к одному значению:

```javascript
const nums = [1, 2, 3, 4];
const sum = nums.reduce((acc, n) => acc + n, 0);  // 10
```

### Когда что использовать?

|Задача|Используй|
|---|---|
|Нужен новый массив|`map`|
|Нужна часть массива|`filter`|
|Нужно одно значение|`reduce`|
|Просто выполнить действие|`forEach`|
|Нужен `break`|`for...of`|

---

## break и continue

### break — выход из цикла

```javascript
for (let i = 0; i < 10; i++) {
  if (i === 5) break;
  console.log(i);  // 0, 1, 2, 3, 4
}
```

### continue — пропуск итерации

```javascript
for (let i = 0; i < 5; i++) {
  if (i === 2) continue;
  console.log(i);  // 0, 1, 3, 4 (2 пропущено)
}
```

### Метки (labels) для вложенных циклов

```javascript
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i === 1 && j === 1) {
      break outer;  // выход из внешнего цикла
    }
    console.log(i, j);
  }
}
// 0 0, 0 1, 0 2, 1 0
```

---

## Iteration Protocols (ES6)

### Iterable Protocol

Объект итерируемый, если имеет метод `[Symbol.iterator]()`:

```javascript
const arr = [1, 2, 3];
const iterator = arr[Symbol.iterator]();

console.log(iterator.next());  // { value: 1, done: false }
console.log(iterator.next());  // { value: 2, done: false }
console.log(iterator.next());  // { value: 3, done: false }
console.log(iterator.next());  // { value: undefined, done: true }
```

### Создание своего итерируемого объекта

```javascript
const range = {
  from: 1,
  to: 5,
  
  [Symbol.iterator]() {
    let current = this.from;
    const last = this.to;
    
    return {
      next() {
        if (current <= last) {
          return { value: current++, done: false };
        }
        return { done: true };
      }
    };
  }
};

for (const num of range) {
  console.log(num);  // 1, 2, 3, 4, 5
}

// Также работает spread:
console.log([...range]);  // [1, 2, 3, 4, 5]
```

### Встроенные итерируемые объекты

- `Array`
- `String`
- `Map`
- `Set`
- `arguments`
- `NodeList` (DOM)
- `TypedArray`

### Что НЕ итерируемо?

```javascript
const obj = { a: 1, b: 2 };

for (const x of obj) {}  // TypeError: obj is not iterable

// Решение — Object.entries():
for (const [key, value] of Object.entries(obj)) {
  console.log(key, value);
}
```

---

## Gotchas

### Модификация массива во время итерации

```javascript
const arr = [1, 2, 3, 4, 5];

// ❌ Опасно:
for (let i = 0; i < arr.length; i++) {
  if (arr[i] % 2 === 0) {
    arr.splice(i, 1);  // Удаляем элемент — индексы сдвигаются!
  }
}
console.log(arr);  // [1, 3, 5]? Нет! [1, 3, 5] — но можем пропустить элементы

// ✅ Лучше:
const filtered = arr.filter(n => n % 2 !== 0);
```

### forEach нельзя прервать

```javascript
// break и return не работают как ожидается:
[1, 2, 3, 4, 5].forEach(n => {
  if (n === 3) return;  // Это не прерывает forEach, только текущий callback
  console.log(n);  // 1, 2, 4, 5
});

// Для прерывания используй for...of:
for (const n of [1, 2, 3, 4, 5]) {
  if (n === 3) break;
  console.log(n);  // 1, 2
}
```

### for...in и порядок свойств

```javascript
const obj = { 2: 'two', 1: 'one', b: 'b', a: 'a' };

for (const key in obj) {
  console.log(key);
}
// Порядок: '1', '2', 'b', 'a'
// Числовые ключи сортируются, строковые — в порядке добавления
```

---

## Interview Questions

- **Разница между for...of и for...in?**

    - `for...of` итерирует по значениям итерируемых объектов
    - `for...in` итерирует по ключам любых объектов
- **Почему for...in не рекомендуется для массивов?**
    
    - Итерирует по всем enumerable свойствам, включая добавленные
    - Возвращает индексы как строки
    - Порядок не гарантирован в старых браузерах
- **Как прервать forEach?**
    
    - Никак. Используй `for...of` с `break` или методы `some()`/`every()`
- **Что такое итерируемый объект?**
    
    - Объект с методом `[Symbol.iterator]()`, который возвращает итератор
- **Разница между while и do...while?**
    
    - `while` проверяет условие до выполнения (может не выполниться ни разу)
    - `do...while` проверяет после (выполнится минимум один раз)
