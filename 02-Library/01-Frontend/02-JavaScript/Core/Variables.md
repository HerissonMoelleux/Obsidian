# Variables

> Переменная - именованная область памяти, предназначенная для хранения информации. var, let, const — три способа объявить переменную, три разных поведения.

---

## Scope — Область видимости

**Область видимости** - это часть кода, где переменные, функции и объекты доступны и могут быть использованы.

Основные области видимости в JavaScript:

- **Глобальная** - Переменные, объявленные вне всех функций и блоков, доступны из любой точки программы
- **Функциональная** - Переменные, объявленные внутри функции, доступны только внутри этой функции
- **Блочная** - Переменные, объявленные внутри фигурных скобок `{}`, доступны только в пределах этого блока

```javascript
let a = 5; 
console.log(a); // Глобальная область видимости 

function scope() {
  let b = 5; 
  console.log(b); // Функциональная область видимости
}

for (let i = 0; i < 5; i++) {
  console.log(i); // Блочная область видимости
}
```

---

## var

### Scope — function-scoped

`var` имеет функциональную область видимости. У неё нет блочной видимости и это причина многих проблем.

```javascript
for (var i = 0; i < 5; i++) {}

console.log(i); // 5 — переменная "утекла" из цикла!
```

### Hoisting — поднятие объявления

**Hoisting** - механизм в JavaScript, при котором объявления переменных и функций "поднимаются" в начало их области видимости перед выполнением кода.

```javascript
console.log(x); // undefined (не ReferenceError!)
var x = 5;
console.log(x); // 5
```

### Переобъявление — разрешено

```javascript
var id = 1;
console.log(id); // 1

var id = 2;
console.log(id); // 2 — данные могут теряться из-за забывчивости
```

### Почему var считается устаревшим?

Главные проблемы `var`:

- Благодаря механизму hoisting переменную можно вызвать до её объявления — это не вызовет ошибок, переменная будет `undefined`
- Переменную можно переобъявлять — легко случайно перезаписать
- Нет блочной области видимости — переменные "утекают" из циклов и условий

---

## let

### Scope — block-scoped

`let` имеет блочную область видимости, т.е. переменная видна только внутри `{}`. Это главное отличие от устаревшей `var`. Преимущество — более предсказуемое поведение.

```javascript
if (true) {
  let x = 5;
}
console.log(x); // ReferenceError: x is not defined
```

### TDZ (Temporal Dead Zone)

**Временная Мёртвая Зона** - это период между началом области видимости и строкой инициализации переменной. В этой зоне переменная существует, но доступ к ней запрещён.

```javascript
// Example 1
console.log(x); // ReferenceError: Cannot access 'x' before initialization
let x = 5;

// Example 2 — TDZ создаётся для каждого scope отдельно
let a = 1;

if (true) {
  console.log(a); // ReferenceError! Внутренняя `a` затеняет внешнюю
  let a = 5;
}
```

### Переобъявление — запрещено

```javascript
let a = 1;
let a = 2; // SyntaxError: Identifier 'a' has already been declared
```

### Переприсваивание — разрешено

```javascript
let a = 5;
a = 1;
console.log(a); // 1
```

---

## const

### Всё как let, плюс...

`const` — переменная очень похожа на `let`: block-scoped, TDZ, нельзя переобъявлять. Но с одним важным отличием.

### Нельзя переприсвоить

Если мы знаем, что значение переменной останется неизменным в течение исполнения программы, лучше использовать `const`.

```javascript
const PI = 3.14159;
PI = 3; // TypeError: Assignment to constant variable
```

### Но можно мутировать объекты!

`const` защищает только **ссылку** на объект, не сам объект.

```javascript
const arr = [1, 2, 3];
arr.push(4);     // [1, 2, 3, 4] — мутация разрешена
arr = [1, 2, 3]; // TypeError — переприсваивание запрещено

const user = { name: 'John' };
user.name = 'Jane'; // Работает! Меняем свойство, не ссылку
user.age = 30;      // Работает! Добавляем свойство
user = {};          // TypeError — нельзя изменить ссылку
```

### Object.freeze() — настоящая иммутабельность?

`Object.freeze()` делает объект "замороженным" — нельзя добавлять, удалять или изменять свойства.

```javascript
const user = { name: 'John', address: { city: 'NYC' } };

Object.freeze(user);

user.name = 'Jane';   // Молча игнорируется (или TypeError в strict mode)
user.age = 30;        // Молча игнорируется
console.log(user.name); // 'John' — не изменилось
```

**НО! freeze — shallow (поверхностный):**

```javascript
user.address.city = 'LA';  // Работает!
console.log(user.address.city); // 'LA' — вложенный объект не заморожен
```

**Deep freeze** — нужно писать самому или использовать библиотеки:

```javascript
function deepFreeze(obj) {
  Object.keys(obj).forEach(key => {
    if (typeof obj[key] === 'object' && obj[key] !== null) {
      deepFreeze(obj[key]);
    }
  });
  return Object.freeze(obj);
}
```

---

## Hoisting Deep Dive

### Что поднимается?

|Что|Поднимается?|Инициализируется?|
|---|---|---|
|`var`|✅ Да|`undefined`|
|`let`|✅ Да (но TDZ!)|❌ Нет|
|`const`|✅ Да (но TDZ!)|❌ Нет|
|`function declaration`|✅ Да|✅ Да (полностью!)|
|`function expression`|Как var/let/const|❌ Нет|

**Важный инсайт:** `let` и `const` тоже поднимаются! Но они находятся в TDZ до строки объявления, поэтому доступ вызывает ReferenceError.

### Визуализация hoisting

```javascript
// Что мы пишем:
console.log(a);
console.log(b);
var a = 1;
let b = 2;

// Как JS "видит" (концептуально):
var a;           // объявление поднято, значение undefined
// let b;        // поднято, но в TDZ — доступ запрещён

console.log(a);  // undefined
console.log(b);  // ReferenceError: Cannot access 'b' before initialization

a = 1;           // присваивание остаётся на месте
let b = 2;       // здесь TDZ заканчивается
```

### Function Declaration vs Expression

```javascript
foo(); // 'foo' — работает!
bar(); // TypeError: bar is not a function

function foo() { return 'foo'; }  // Declaration — поднимается полностью
var bar = function() { return 'bar'; };  // Expression — только var поднимается
```

**Почему bar выдаёт TypeError, а не ReferenceError?**

```javascript
// JS видит так:
var bar;              // bar = undefined
bar();                // undefined() — TypeError!
bar = function() {};  // присваивание происходит позже
```

---

## TDZ (Temporal Dead Zone)

### Что такое TDZ?

Зона от начала scope до строки объявления переменной, где переменная существует, но недоступна.

### Почему TDZ существует?

Две причины:

1. **Защита от багов** — использование переменной до инициализации почти всегда ошибка
2. **const должен работать правильно** — если бы const был доступен до инициализации как undefined, это нарушило бы семантику "константы"

```javascript
// Без TDZ было бы возможно:
console.log(API_KEY);  // undefined — это баг, не фича!
const API_KEY = 'secret';
```

### Визуализация TDZ

```javascript
{
  // ← TDZ для x начинается здесь
  
  console.log(x); // ReferenceError
  
  let x = 5; // ← TDZ заканчивается здесь
  
  console.log(x); // 5
}
```

---

## Scope Chain

### Как JS ищет переменную?

**Алгоритм:**

1. Ищет в текущем scope
2. Не нашёл → идёт во внешний scope
3. Повторяет до глобального scope
4. Не нашёл в глобальном → ReferenceError

```javascript
const outer = 'outer';

function test() {
  const inner = 'inner';
  console.log(outer); // 'outer' — нашёл во внешнем scope
  console.log(inner); // 'inner' — нашёл в текущем scope
}
```

### Lexical Scope

Scope определяется **где функция написана**, а не где вызвана:

```javascript
const x = 'global';

function outer() {
  const x = 'outer';
  
  function inner() {
    console.log(x);  // 'outer' — смотрит где объявлена, не где вызвана
  }
  
  return inner;
}

const fn = outer();
fn();  // 'outer', не 'global'
```

---

## Best Practices

### const по умолчанию

Использовать `const` по умолчанию — хорошая практика:

- Улучшает читаемость — сразу видно, что значение не меняется
- Дополнительная безопасность — случайное переприсваивание вызовет ошибку
- Помогает писать более функциональный код

### let когда нужно переприсвоить

```javascript
// Циклы
for (let i = 0; i < 10; i++) { }

// Накопление значения
let total = 0;
items.forEach(item => { total += item.price; });

// Условное присваивание
let status;
if (user.isAdmin) {
  status = 'admin';
} else {
  status = 'user';
}
// Хотя лучше: const status = user.isAdmin ? 'admin' : 'user';
```

### var — никогда?

Почти никогда. Единственный легитимный случай — поддержка очень старых браузеров (IE10 и ниже), но это уже неактуально в 2024+.

### Объявляй в начале scope

Для читаемости и чтобы избежать TDZ-сюрпризов объявляй переменные в начале блока.

---

## Gotchas

### var и глобальный объект window

`window` - глобальный объект браузера, он содержит в себе: 

- Все встроенные функции (`alert`, `setTimeout`, `fetch`)
- Информацию о браузере (`navigator`, `location`, `history`)
- Размеры окна (`innerWidth`, `innerHeight`)
- И многое другое

`var` в глобальной области создаёт свойство на объекте `window`, что может перезаписать встроенные методы:
```javascript
var alert = 'Important!';
alert('Hello');  // TypeError: alert is not a function

var location = 'New York';
// window.location (URL страницы) теперь сломан!

// let и const безопасны — не создают свойства на window:
let fetch = 'data';
window.fetch('/api');  // Работает, встроенный fetch не затронут
```

**Опасные имена переменных:** `name`, `top`, `status`, `length`, `open`, `close`, `location`, `alert`, `confirm`, `prompt`

### var в цикле + setTimeout

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// Output: 3, 3, 3

// Почему? var — function-scoped, одна переменная i на все итерации.
// К моменту выполнения setTimeout цикл уже завершён, i = 3
```

### Как исправить с let

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// Output: 0, 1, 2

// Почему? let — block-scoped, каждая итерация создаёт новую переменную i
```

### const с объектами

```javascript
const user = { name: 'John' };
user.name = 'Jane'; // Работает! Меняем свойство, не ссылку
user = {};          // TypeError: Assignment to constant variable
```

### TDZ с внутренней переменной

```javascript
let x = 1;

function foo() {
  console.log(x); // ReferenceError!
  let x = 2;
}

foo();
// Внутренняя let x затеняет внешнюю, но находится в TDZ
```

---

## Interview Questions

- **Чем отличаются var, let, const?**
	
    - var: function-scoped, hoisting с undefined, можно переобъявлять
    - let: block-scoped, TDZ, нельзя переобъявлять, можно переприсваивать
    - const: как let, но нельзя переприсваивать
- **Что такое hoisting?**
	
    - Механизм "поднятия" объявлений в начало scope перед выполнением кода
- **Что такое TDZ?**
	
    - Temporal Dead Zone — период от начала scope до объявления let/const, когда переменная существует, но недоступна
- **Почему `const obj = {}; obj.x = 1;` работает?**
	
    - const защищает ссылку, не содержимое объекта
- **Что выведет цикл с var и setTimeout?**
	
    - 3, 3, 3 — потому что var function-scoped, одна переменная на все итерации
