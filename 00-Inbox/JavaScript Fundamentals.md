# 📚 JavaScript Fundamentals - Конспект-Шпаргалка

> **Роль**: Team Lead → Стажёр  
> **Цель**: Систематизация знаний на пути к Senior JavaScript Developer  
> **Источник**: Практические задачи CodeWars и экспериментальный код

---

## 🎯 Оглавление

1. [Работа с массивами](#работа-с-массивами)
2. [Работа со строками](#работа-со-строками)
3. [Циклы и итерации](#циклы-и-итерации)
4. [Работа с числами](#работа-с-числами)
5. [Объекты и структуры данных](#объекты-и-структуры-данных)
6. [Функции и стрелочные функции](#функции-и-стрелочные-функции)
7. [ООП и классы](#ооп-и-классы)
8. [Асинхронное программирование](#асинхронное-программирование)
9. [Event Loop и Microtasks](#event-loop-и-microtasks)
10. [Web APIs](#web-apis)
11. [Алгоритмы и паттерны](#алгоритмы-и-паттерны)

---

## 📊 Работа с массивами

### Основные методы массивов

#### `.filter()` - фильтрация элементов

```javascript
// Фильтрует элементы по условию, возвращает новый массив
const friends = ["Arthur", "Sam", "Ryan"];
const result = friends.filter((item) => item.length === 4);
// ['Ryan']
```

**Когда использовать**: Когда нужно получить подмножество элементов, соответствующих условию.

---

#### `.map()` - трансформация элементов

```javascript
// Преобразует каждый элемент массива
const array = [1, 2, 3, -4, 5];
const result = array.map((item) => item * -1);
// [-1, -2, -3, 4, -5]
```

**Когда использовать**: Для преобразования всех элементов массива по одному правилу.

---

#### `.reduce()` - сведение к одному значению

```javascript
// Сводит массив к одному значению (сумма, произведение и т.д.)
const numbers = [7, 15, 5];
const product = numbers.reduce((acc, num) => acc * num);
// 525

// Можно использовать для подсчета вхождений
const word = "Kseniia";
const charCount = word.split("").reduce((acc, char) => {
  acc[char] = acc[char] ? acc[char] + 1 : 1;
  return acc;
}, {});
// { K: 1, s: 1, e: 1, n: 1, i: 2, a: 1 }
```

**Когда использовать**: Для агрегации данных (сумма, произведение, группировка).

**⚠️ Важно**: Второй аргумент - начальное значение аккумулятора (`{}` в примере выше).

---

#### `.sort()` - сортировка

```javascript
// МУТИРУЕТ исходный массив!
const array = ["Telescopes", "Glasses", "Eyes", "Monocles"];
array.sort((a, b) => a.length - b.length);
// Сортировка по длине строк

const numbers = [1, 2, 10, 4, 5];
numbers.sort((a, b) => a - b); // Числовая сортировка по возрастанию
// [1, 2, 4, 5, 10]
```

**⚠️ Важно**:

- `.sort()` изменяет оригинальный массив
- Для чисел обязательно использовать функцию сравнения `(a, b) => a - b`

---

#### `.find()` - поиск первого элемента

```javascript
const people = [
  { name: "Ksenia", age: 17, sex: "female" },
  { name: "Arthur", age: 18, sex: "male" },
];

const female = people.find((person) => person.sex === "female");
// {name: 'Ksenia', age: 17, sex: 'female'}
```

**Когда использовать**: Когда нужен первый элемент, удовлетворяющий условию.

---

#### `.every()` - проверка всех элементов

```javascript
// Проверяет, удовлетворяют ли ВСЕ элементы условию
function isPangram(string) {
  return "abcdefghijklmnopqrstuvwxyz"
    .split("")
    .every((x) => string.toLowerCase().includes(x));
}
```

**Когда использовать**: Когда нужно убедиться, что все элементы соответствуют условию.

---

#### `.slice()` - извлечение части массива

```javascript
const arr = [1, 2, 3, 4, 5];
const leftPart = arr.slice(0, 2); // [1, 2] (до индекса 2, не включая)
const rightPart = arr.slice(3); // [4, 5] (от индекса 3 до конца)
```

**⚠️ Важно**: Не изменяет оригинальный массив, создаёт новый.

---

#### `.splice()` - удаление/добавление элементов

```javascript
// МУТИРУЕТ исходный массив!
const numbers = [1, 2, 3, 4, 5];
numbers.splice(2, 1); // Удаляет 1 элемент начиная с индекса 2
// [1, 2, 4, 5]
```

**⚠️ Важно**: Изменяет оригинальный массив.

---

#### `.indexOf()` - поиск индекса элемента

```javascript
const arr = ["a", "b", "c"];
const index = arr.indexOf("b"); // 1
```

---

#### `.push()` - добавление элемента в конец

```javascript
const arr = [1, 2];
arr.push(3); // [1, 2, 3]
```

---

#### `.flatMap()` - комбинация map + flat

```javascript
// Выполняет map и затем flatten на один уровень
const gifts = [
  { toy: "car", quantity: 3 },
  { toy: "doll", quantity: 1 },
];

const result = gifts.flatMap((obj) => {
  if (obj.quantity > 0) {
    return Array.from({ length: obj.quantity }, () => obj.toy);
  }
  return [];
});
// ['car', 'car', 'car', 'doll']
```

**Когда использовать**: Когда после map нужно "выровнять" массив на один уровень.

---

### Работа с индексами и обход

#### Прямой обход

```javascript
for (let i = 0; i < array.length; i++) {
  console.log(array[i]);
}
```

#### Обратный обход

```javascript
for (let i = array.length - 1; i >= 0; i--) {
  console.log(array[i]);
}
```

#### `for...of` - итерация по значениям

```javascript
const arr = [1, 2, 10, 4, 5];
for (let number of arr) {
  console.log(number); // 1, 2, 10, 4, 5
}
```

**Когда использовать**: Когда нужны только значения, без индексов.

---

### Копирование массивов

#### Spread оператор `...`

```javascript
const original = [1, 2, 3];
const copy = [...original]; // Поверхностная копия
```

**⚠️ Важно**: Создаёт **поверхностную** копию (shallow copy). Вложенные объекты копируются по ссылке.

---

### Двумерные массивы (матрицы)

```javascript
const matrix = [
  [10, 0],
  [3, 5],
  [5, 8],
];
let result = 0;

for (let i = 0; i < matrix.length; i++) {
  result += matrix[i][0] - matrix[i][1];
}
// Обращение: matrix[строка][столбец]
```

---

## 📝 Работа со строками

### Основные методы

#### `.split()` - разбиение строки на массив

```javascript
const str = "Hello World";
const words = str.split(" "); // ['Hello', 'World']
const chars = str.split(""); // ['H', 'e', 'l', 'l', 'o', ...]
```

---

#### `.join()` - соединение массива в строку

```javascript
const arr = ["H", "e", "l", "l", "o"];
const str = arr.join(""); // "Hello"
```

---

#### `.toLowerCase()` / `.toUpperCase()`

```javascript
const str = "Hello";
str.toLowerCase(); // "hello"
str.toUpperCase(); // "HELLO"
```

---

#### `.includes()` - проверка наличия подстроки

```javascript
const str = "Hello World";
str.includes("World"); // true
str.includes("world"); // false (регистрозависимо!)
```

---

#### `.charCodeAt()` - код символа

```javascript
"a".charCodeAt(0); // 97
"A".charCodeAt(0); // 65

// Пример: сумма позиций букв в алфавите
let word = "taxi";
let sum = 0;
for (let i = 0; i < word.length; i++) {
  sum += word[i].charCodeAt(0) - "a".charCodeAt(0) + 1;
}
```

---

#### `.repeat()` - повторение строки

```javascript
"*".repeat(3); // "***"
" ".repeat(2); // "  "
```

---

#### `.substring()` - извлечение подстроки

```javascript
const str = "Hello World";
str.substring(0, 5); // "Hello"
str.substring(6); // "World"
```

---

#### `.match()` - поиск по регулярному выражению

```javascript
const word = "AmiArhKse";
const result = [];

for (let i = 0; i < word.length; i++) {
  if (word[i].match(/[A-Z]/)) {
    // Заглавные буквы
    result.push(i);
  }
}
// [0, 3, 6]
```

---

### Паттерны работы со строками

#### Разбить camelCase

```javascript
function solution(string) {
  return string
    .split("")
    .map((letter) => {
      if (letter === letter.toUpperCase()) {
        return ` ${letter}`;
      }
      return letter;
    })
    .join("");
}

solution("camelCaseTest"); // "camel Case Test"
```

---

#### Проверка на Pangram (все буквы алфавита)

```javascript
// Способ 1: через every
function isPangram(string) {
  return "abcdefghijklmnopqrstuvwxyz"
    .split("")
    .every((x) => string.toLowerCase().includes(x));
}

// Способ 2: через Set
const isPangram = (string) => {
  let result = Array.from(new Set(string.toLowerCase())).sort().join("");
  result = result.substring(result.indexOf("a"), result.length);
  return result === "abcdefghijklmnopqrstuvwxyz";
};
```

---

## 🔄 Циклы и итерации

### `for` - классический цикл

```javascript
for (let i = 0; i < array.length; i++) {
  // код
}
```

**Когда использовать**: Когда нужен контроль над индексом.

---

### `while` - цикл с предусловием

```javascript
let a = 13;
let result = "";

while (a > 0) {
  if (a % 2 === 0) {
    result = "0" + result;
  } else {
    result = "1" + result;
  }
  a = Math.floor(a / 2);
}
// Конвертация числа в двоичную систему
```

**Когда использовать**: Когда количество итераций заранее неизвестно.

---

### `for...of` - итерация по значениям

```javascript
for (let number of arr) {
  console.log(number);
}
```

**Когда использовать**: Когда нужны только значения.

---

### `for...in` - итерация по ключам объекта

```javascript
const objArray = { 1: 2, 2: 1, 10: 1 };

for (let key in objArray) {
  console.log(key, objArray[key]);
}
```

**Когда использовать**: Для перебора свойств объекта.

**⚠️ Важно**: Возвращает ключи как строки!

---

## 🔢 Работа с числами

### `Math` объект

#### `Math.floor()` - округление вниз

```javascript
Math.floor(5.9); // 5
Math.floor(a / 2); // Целочисленное деление
```

---

#### `Math.trunc()` - отбрасывание дробной части

```javascript
Math.trunc(5.9); // 5
Math.trunc(-5.9); // -5
```

---

#### `Math.pow()` - возведение в степень

```javascript
Math.pow(2, 3); // 8 (2³)

// Конвертация из двоичной системы
const binaryArray = [1, 1, 1, 1];
let result = 0;
for (let i = binaryArray.length - 1; i >= 0; i--) {
  let power = binaryArray.length - 1 - i;
  if (binaryArray[i] === 1) {
    result += Math.pow(2, power);
  }
}
```

---

#### `Math.abs()` - абсолютное значение

```javascript
Math.abs(-5); // 5
Math.abs(nums[i] - nums[j]); // Разница без знака
```

---

### Операции с числами

#### Остаток от деления `%`

```javascript
13 % 2; // 1 (нечетное)
10 % 2; // 0 (четное)

// Получение последней цифры числа
let digit = num % 10;
```

---

#### Целочисленное деление

```javascript
let num = 123;
num = Math.floor(num / 10); // 12 (отбросили последнюю цифру)
```

---

### Преобразование типов

#### Строка → Число

```javascript
Number("123"); // 123
parseInt("123"); // 123
+"123"; // 123
```

---

#### Проверка на число

```javascript
isNaN("hello"); // true
isNaN("123"); // false
!isNaN(parseInt(str)); // Проверка, что строка содержит число
```

---

### Алгоритмы с числами

#### Разворот числа

```javascript
function reverseNumber(n) {
  let reversedNumber = 0;

  while (n > 0) {
    let digit = n % 10; // Берём последнюю цифру
    reversedNumber = reversedNumber * 10 + digit; // Добавляем в результат
    n = Math.floor(n / 10); // Убираем последнюю цифру
  }

  return reversedNumber;
}
// 123 → 321
```

---

#### Персистентность числа (умножение цифр до однозначного)

```javascript
function persistence(num) {
  function multiplyDigits(n) {
    let result = 1;
    while (n > 0) {
      let digit = n % 10;
      n = Math.trunc(n / 10);
      result *= digit;
    }
    return result;
  }

  let count = 0;
  while (num > 9) {
    count++;
    num = multiplyDigits(num);
  }

  return count;
}

persistence(39); // 39 → 27 → 14 → 4 (3 шага)
```

---

## 🗂️ Объекты и структуры данных

### Создание и работа с объектами

#### Литеральная нотация

```javascript
const languages = {
  english: "Welcome",
  russian: "Добро пожаловать",
  dutch: "Welkom",
};

// Доступ к свойствам
languages["english"]; // 'Welcome'
languages.english; // 'Welcome'
languages["unknown"] || languages["english"]; // Значение по умолчанию
```

---

#### Динамическое создание объекта через `reduce`

```javascript
const array = [1, 1, 2];

const objArray = array.reduce((acc, number) => {
  acc[number] = acc[number] ? acc[number] + 1 : 1;
  return acc;
}, {});
// { 1: 2, 2: 1 } - подсчет вхождений
```

---

### `Set` - множество уникальных значений

```javascript
const word = "hello";
const uniqueChars = new Set(word.toLowerCase());
// Set { 'h', 'e', 'l', 'o' }

Array.from(uniqueChars); // ['h', 'e', 'l', 'o']
```

**Когда использовать**: Для удаления дубликатов или проверки уникальности.

---

### Деструктуризация и обмен значений

#### Обмен переменных без временной

```javascript
let a = 1,
  b = 2;
[a, b] = [b, a]; // a = 2, b = 1
```

---

## ⚡ Функции и стрелочные функции

### Обычные функции

```javascript
function greet(name) {
  return `Hello, ${name}`;
}
```

---

### Стрелочные функции

#### Краткая форма (неявный return)

```javascript
const sum = (a, b) => a + b;
```

---

#### Развернутая форма (с блоком кода)

```javascript
const filter = (arr) => {
  let result = [];
  for (let item of arr) {
    if (item > 0) result.push(item);
  }
  return result;
};
```

---

### Function Expression vs Function Declaration

```javascript
// Declaration - поднимается (hoisting)
function declared() {}

// Expression - не поднимается
const expressed = function () {};
const arrow = () => {};
```

---

### Вложенные функции

```javascript
function towerBuilderMy(nFloors) {
  let funcFloor = (n, currentFloor) => {
    // Внутренняя функция
    let result = "";
    // ... логика
    return result;
  };

  for (let i = 0; i < nFloors; i++) {
    resultArray.push(funcFloor(nFloors * 2 - 1, i));
  }
}
```

**Когда использовать**: Для инкапсуляции логики внутри функции.

---

## 🎓 ООП и классы

### ES6 классы

```javascript
class Fighter {
  // Приватные поля (Private Class Fields)
  #name;
  #damagePerAttack;

  // Геттеры для чтения приватных полей
  get name() {
    return this.#name;
  }
  get damagePerAttack() {
    return this.#damagePerAttack;
  }

  // Конструктор
  constructor(name, health, damagePerAttack) {
    this.#name = name;
    this.#damagePerAttack = damagePerAttack;
    this.health = health; // Публичное свойство
  }
}

const fighter1 = new Fighter("Lew", 10, 2);
console.log(fighter1.name); // 'Lew' (через геттер)
// fighter1.#name - ERROR! Приватное поле
```

---

### Ключевые концепции ООП

#### 1. **Приватные поля** (`#field`)

- Доступны только внутри класса
- Синтаксис: `#fieldName`

#### 2. **Геттеры** (`get`)

- Позволяют читать приватные поля как обычные свойства
- Синтаксис: `get propertyName() { return this.#field; }`

#### 3. **Конструктор** (`constructor`)

- Вызывается при создании экземпляра класса (`new Class()`)
- Инициализирует свойства объекта

---

## ⏱️ Асинхронное программирование

### Промисы (Promises)

#### Базовый синтаксис

```javascript
Promise.resolve().then(() => {
  console.log("promise 1");
});
```

---

### `async/await` - современный подход

#### Fetch API с async/await

```javascript
async function fetchPosts() {
  try {
    const response = await fetch("https://api.example.com/posts");
    const json = await response.json();
    console.log(json);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}
```

---

#### Проверка статуса ответа

```javascript
async function getUser(userId) {
  try {
    const response = await fetch(`https://api.example.com/users/${userId}`, {
      method: "GET",
      headers: { Authorization: "Bearer token" },
    });

    // Проверка успешности запроса
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const user = await response.json();
    return user;
  } catch (error) {
    console.error("Error fetching user:", error.message);
  }
}
```

**⚠️ Важно**:

- `fetch` не выбрасывает ошибку при HTTP 404/500
- Нужна явная проверка `response.ok`

---

### Fetch API - классический подход с `.then()`

```javascript
fetch("https://jsonplaceholder.typicode.com/users")
  .then((response) => response.json())
  .then((json) => {
    json.forEach((user) => {
      console.log(user.name);
    });
  });
```

---

### Конфигурация fetch

```javascript
fetch(url, {
  method: "GET", // GET, POST, PUT, DELETE
  headers: {
    // Заголовки
    "Content-Type": "application/json",
    Authorization: "Bearer token",
  },
  body: JSON.stringify(data), // Тело запроса (для POST/PUT)
});
```

---

## 🔁 Event Loop и Microtasks

### Очередь выполнения в JavaScript

#### Порядок выполнения:

1. **Синхронный код** (обычные `console.log`)
2. **Microtasks** (промисы, `queueMicrotask`)
3. **Macrotasks** (`setTimeout`, `setInterval`)

---

### Пример работы Event Loop

```javascript
console.log("1"); // Синхронный код - выполнится первым

setTimeout(() => {
  console.log("setTimeout 1"); // Macrotask - выполнится последним
}, 0);

Promise.resolve().then(() => {
  console.log("promise 1"); // Microtask - выполнится после синхронного кода
});

queueMicrotask(() => {
  console.log("queueMicrotask 1"); // Microtask
});

console.log("4"); // Синхронный код

// Вывод: 1, 4, promise 1, queueMicrotask 1, setTimeout 1
```

---

### Вложенные асинхронные операции

```javascript
setTimeout(() => {
  console.log("setTimeout 1");

  Promise.resolve().then(() => {
    console.log("promise setTimeout 1"); // Microtask внутри Macrotask
  });

  queueMicrotask(() => {
    console.log("queueMicrotask setTimeout 1");
  });
}, 0);

setTimeout(() => {
  console.log("setTimeout 2"); // Следующий Macrotask
}, 0);

// Вывод: setTimeout 1, promise setTimeout 1, queueMicrotask setTimeout 1, setTimeout 2
```

**💡 Правило**: После каждого Macrotask выполняются ВСЕ Microtasks.

---

## 🌐 Web APIs

### DOM манипуляции

#### Получение элементов

```javascript
const title = document.getElementById("title");
const userList = document.querySelector("#user-list");
```

---

#### Создание и добавление элементов

```javascript
const listItem = document.createElement("li");
listItem.textContent = "Hello";
userList.appendChild(listItem);
```

---

#### Изменение содержимого

```javascript
title.innerText = "New Title";
title.innerHTML = "<span>HTML content</span>";
```

---

### MutationObserver - отслеживание изменений DOM

```javascript
const title = document.getElementById("title");
const button = document.getElementById("button");

let count = 0;
button.onclick = function () {
  count++;
  title.innerText = count.toString();

  Promise.resolve().then(() => {
    console.log("promise onclick");
  });

  setTimeout(() => {
    console.log("setTimeout onclick");
  }, 0);
};

// Отслеживание изменений в DOM
const mutationObserver = new MutationObserver((mutations) => {
  console.log("DOM changed!");
});

mutationObserver.observe(title, {
  childList: true, // Отслеживать добавление/удаление дочерних элементов
  subtree: true, // Отслеживать изменения во всех потомках
  attributeOldValue: true, // Сохранять старые значения атрибутов
});
```

**Когда использовать**: Для реакции на изменения DOM (например, в библиотеках или фреймворках).

---

## 🧩 Алгоритмы и паттерны

### Snowball Algorithm - перемещение нулей

```javascript
function moveZeros(arr) {
  let nonZeroIndex = 0;

  // Первый проход: перемещаем все ненулевые элементы в начало
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] !== 0) {
      arr[nonZeroIndex] = arr[i];
      nonZeroIndex++;
    }
  }

  // Второй проход: заполняем оставшиеся позиции нулями
  for (let i = nonZeroIndex; i < arr.length; i++) {
    arr[i] = 0;
  }

  return arr;
}
// [1, 0, 2, 0, 3] → [1, 2, 3, 0, 0]
```

**Применение**: Эффективная перестановка элементов in-place за O(n).

---

### Two Pointers - два указателя

```javascript
// Поиск индекса баланса массива
let arr = [1, 2, 3, 4, 3, 2, 1];

for (let i = 0; i < arr.length; i++) {
  let leftArr = arr.slice(0, i);
  let sumLeft = leftArr.length === 0 ? 0 : leftArr.reduce((a, b) => a + b);

  let rightArr = arr.slice(i + 1);
  let sumRight = rightArr.length === 0 ? 0 : rightArr.reduce((a, b) => a + b);

  if (sumLeft === sumRight) {
    console.log(i); // Индекс баланса
  }
}
```

---

### Switch с условиями

```javascript
function monthQuarter(month) {
  let result = 0;
  switch (
    true // ← Используем switch(true) для условий
  ) {
    case month < 4:
      result = 1;
      break;
    case month < 7:
      result = 2;
      break;
    case month < 10:
      result = 3;
      break;
    case month < 13:
      result = 4;
      break;
  }
  return result;
}
```

**💡 Хитрость**: `switch(true)` позволяет использовать условные выражения в `case`.

---

### Array.from() - создание массива

```javascript
// Создание массива заданной длины с элементами
Array.from({ length: 3 }, () => "car");
// ['car', 'car', 'car']

// С индексами
Array.from({ length: 5 }, (_, i) => i);
// [0, 1, 2, 3, 4]
```

---

### Работа с подстроками в массивах

```javascript
let a1 = ["arp", "live", "strong"];
let a2 = ["lively", "alive", "harp", "sharp", "armstrong"];

function inArray(a1, a2) {
  let resultArr = [];

  for (let i = 0; i < a1.length; i++) {
    for (let j = 0; j < a2.length; j++) {
      if (a2[j].includes(a1[i]) && !resultArr.includes(a1[i])) {
        resultArr.push(a1[i]);
      }
    }
  }

  return resultArr;
}
// ['arp', 'live', 'strong'] - все найдены в a2
```

---

## 📌 Ключевые Best Practices

### 1. Изменяемость (Mutability)

| Метод                  | Мутирует оригинал? | Создаёт копию? |
| ---------------------- | ------------------ | -------------- |
| `.push()`, `.pop()`    | ✅ Да              | ❌ Нет         |
| `.sort()`, `.splice()` | ✅ Да              | ❌ Нет         |
| `.map()`, `.filter()`  | ❌ Нет             | ✅ Да          |
| `.slice()`, `[...arr]` | ❌ Нет             | ✅ Да          |

**⚠️ Важно**: Всегда проверяй, мутирует ли метод массив!

---

### 2. Выбор метода массива

- **Трансформация** → `.map()`
- **Фильтрация** → `.filter()`
- **Агрегация** → `.reduce()`
- **Поиск** → `.find()` / `.findIndex()`
- **Проверка** → `.every()` / `.some()`

---

### 3. Асинхронный код

```javascript
// ❌ Плохо
fetch(url)
  .then((r) => r.json())
  .then((data) => {
    /* ... */
  });

// ✅ Хорошо
async function getData() {
  try {
    const response = await fetch(url);
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Error:", error);
  }
}
```

---

### 4. Работа с объектами

```javascript
// Проверка наличия свойства
const obj = { a: 1 };
"a" in obj; // true
obj.hasOwnProperty("a"); // true

// Значение по умолчанию
const value = obj.unknown || "default";
```

---

## 🎯 Roadmap к Senior JavaScript Developer

### Что ты уже освоил ✅

1. ✅ Основы массивов (методы высшего порядка)
2. ✅ Работа со строками
3. ✅ Циклы и итерации
4. ✅ Объекты и структуры данных
5. ✅ Функции и стрелочные функции
6. ✅ Асинхронное программирование (Promise, async/await)
7. ✅ Event Loop и Microtasks
8. ✅ Базовые алгоритмы
9. ✅ ООП и классы (ES6)
10. ✅ Web APIs (DOM, Fetch, MutationObserver)

---

### Над чем работать дальше 🚀

#### 1. **Углубленное понимание JavaScript**

- Замыкания (Closures)
- Контекст выполнения (`this`)
- Прототипное наследование
- Модули (ES6 Modules)

#### 2. **Продвинутая асинхронность**

- `Promise.all()`, `Promise.race()`
- Обработка ошибок в асинхронном коде
- Отмена запросов (`AbortController`)

#### 3. **Структуры данных и алгоритмы**

- Хеш-таблицы
- Стек и Очередь
- Рекурсия
- Динамическое программирование

#### 4. **Функциональное программирование**

- Чистые функции
- Композиция функций
- Каррирование (Currying)

#### 5. **Тестирование**

- Unit тесты (Jest, Vitest)
- TDD подход

#### 6. **Современные инструменты**

- TypeScript
- Сборщики (Webpack, Vite)
- Git (продвинутое использование)

#### 7. **Паттерны проектирования**

- Singleton, Factory, Observer
- SOLID принципы

---

## 💡 Советы от Team Lead

### 1. **Читай чужой код**

Изучай решения других разработчиков на CodeWars. Часто там есть элегантные решения в одну строку.

### 2. **Практикуй рефакторинг**

Возвращайся к старым задачам и переписывай их более чистым и эффективным способом.

### 3. **Понимай, а не запоминай**

Не зубри методы - понимай, ЧТО они делают и КОГДА их использовать.

### 4. **Думай о производительности**

- O(n) vs O(n²)
- Избегай лишних циклов
- Используй правильные структуры данных

### 5. **Пиши чистый код**

- Понятные имена переменных
- Маленькие функции (одна задача)
- Комментируй сложную логику

---

## 📖 Полезные ресурсы

1. **MDN Web Docs** - документация по JavaScript
2. **JavaScript.info** - отличный туториал
3. **Eloquent JavaScript** - книга для понимания концепций
4. **CodeWars** - практика алгоритмов
5. **LeetCode** - подготовка к собеседованиям

---

**Помни**: Путь к Senior - это марафон, а не спринт. Ты уже на правильном пути! 💪

> _"Code is like humor. When you have to explain it, it's bad."_ - Cory House
