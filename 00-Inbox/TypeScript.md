# TypeScript: notes on the lecture

## Lecture plan

- **Самое главное:** научиться понимать, а не писать код интуитивно по заученным шаблонам.
- [x] Проблемы JavaScript, вид типизации, как устроена работа с примитивами и объектами, хранение в памяти.
- [x] Что представляет из себя TypeScript? Что такое яваная/неявная, статическая и структурная типизация?
- [x] Как воспринимать типы? Работа с множествами.
- [x] Поделим типы на подгруппы и разберемся с каждой.
- [x] Разберем понятия супертип и надтип.
- [x] `never`, `unknown`, `any`, `void` - в концепции супертипов и надтипов. Учимся действительно понимать, как они устроены.
- [x] Разберем дженерики и условные типы.
- Рассмотрим концепцию сужения и расширения типов, и то какими способами этого можно добиться.
- Поговорим о преобразовании типов, хорошие и плохие практики. Рассмотрим опасные примеры.
- Рассмотрим различные операторы.
- `Infer` и как его понять и начать готовить.
- Конфигурация проекта и пример большого эталонного проекта.


## Problems of JavaScript

- **JavaScript - язык со слабой динамической типизацией**
	
	- Слабая типизация JavaScript позволяет работать с разными типами данных, при этом неявно преобразуя их ([[Coercion]]).
	- Динамическая типизация определяет тип в `runtime` т.е. во время выполнения программы, а не на этапе компиляции и написания кода.

- Сложность в поддержке больших проектов (много данных, нет четкого описания)
- На этапе написания кода отлиавливать проблемы с типами приходится в уме
- Усложняется дебаг и тестирование кода
- Усложняется анализ кода разработчиком. Требуется дополнительная когнитивная нагрузка для анализа кода
- Отсутствие адекватного автокомплита в среде разработки

## TypeScript and Data Types

- **TypeScript - язык программирования со статической типизицией(явной или выводимой + структурной), вдобавок это является надмножеством JavaScript** 
	
	- Статическая - типы проверяются на этапе компиляции, а не во время выполнения 
	- Явная типизация:  `const variable: number = 5;` 
	- Выводимая типизация: `const variable = 5; // TS сам выведет number`
	- Структурная типизация позволяет взаимозаменять типы с одинаковыми полями:
``` TypeScript
type User = {
	firstname: string;
	lastname: string;
}

type Person = {
	firstname: string;
	lastname: string;
}

// User и Person - Взаимозаменяемы(!)
```
### Типы данных в JavaScript

- **Примитивы (7 типов):**
	
	- `String`
	- `Number`
	- `Bigint`
	- `Boolean`
	- `Undefined`
	- `Null`
	- `Symbol`
``` JavaScript 
const zero = 'value';
const first = 5;
const second = first; 
// Значение из first копируется т.е. В stack будет: second = 5, second хранит то же значение(!)
```
- **Объекты (ссылочные типы):
	
	- Объекты
	- Функции
	- Массивы
	- `Date` 
	- И т.д. 
``` JavaScript
const user = {
	username: "Amir",
	password: "Secret",
	// В stack будет храниться адрес(!) user'а в памяти(heap)
}
```

### Типы данных в TypeScript

- **Примитивы** - Такие же как в JavaScript, без изменений
- **Составные типы** - Нужны чтобы мы могли комбинировать примитвы в более сложные структуры
	
	- `interface` - предназначены для описания формы объекта. есть уникальная фишка слияния (`Declaration Merging`).
	- `type` - более универсальный, он может быть не только объектом, но и примитивом, объединением или кортежем.
``` TypeScript
// Merging
interface User { name: string; }
interface User { age: number; }

// Итоговый User будет иметь и name, и age
```
- **Специальные типы** - Описывают типы выходящие за рамки примитивов и объектов
	
	- `any` - самый опасный тип, он отключает проверку типов для переменной, является супертипом и подтипом одновременно.
	- `unknown` - "безопасный `any`" работает также, но требует проверку перед работой с переменной, является супертипом для всех, но не может быть подтипом.
	- `never` - невозможное значение, является подтипом для всех, но не может быть супертипом.
	- `void` - используется для функций, которые ничего не возвращают
- **Литералы** - Позволяют использовать конкретные значения в качестве типов
	
	- Строковые литералы
	- Числовые литералы
	- Булевы литералы
	- Шаблонные строковые литералы
	- Составные литералы
``` TypeScript
type Color = "red" | "green" | "blue"; // Строковый литерал
const color: Color = "red";

type EvenNumbers = 2 | 4 | 8; // Числовой литерал

type Boolean = true; // Булев литерал

type Side = "left" | "right" | "top" | "bottom"; // Шаблонный строковый литерал
type Margin = `margin-${Side}`; 
// Итоговый тип Margin это: "margin-left" | "margin-right" | "margin-top" | "margin-bottom"

const config = {
  method: "GET", 
  port: 8080
} as const; // Составной литерал, если использовать иначе, то method будет определен как строка

// Теперь тип config.method — это не string, а конкретно "GET"
// А config.port — это конкретно 8080
```
- **Generic types** - Способ создать компонент (функцию, класс, интерфейс), который может работать с различными типами, не теряя информации о них
	
	 - `Generic` 
	 - `Constraints` - Иногда Generic T слишком широкий, это создает ограничения на использование различных методов (`.length`), чтобы решить это мы испольуем `extends` и ограничиваем типы для Generic
	 - `Conditional Types` - По сути тернарны оператор, который позволяет выбрать нужный тип 
``` TypeScript
// Example 1 (Problems)
function echo(arg: any): any {
  return arg;
}
// Мы потеряли тип. Передали строку, получили any. 
// TS не подскажет методы строки.

function echo<T>(arg: T): T {
  return arg;
}

const result = echo("Hello"); 
// Теперь TS знает: result — это string. 
// T автоматически превратилось в string.
```
	
``` TypeScript
// Example 2 (Constraints)
interface ILength {
  length: number;
}

// Говорим: "T может быть чем угодно, НО оно обязано расширять ILength"
function logLength<T extends ILength>(arg: T): void {
  console.log(arg.length);
}

logLength("Привет"); // ОК
logLength([1, 2, 3]); // ОК 
// logLength(100);    // Error: У числа нет length
```
	
``` TypeScript
type IsString<T> = T extends string ? "Да, это строка" : "Нет, не строка";

type A = IsString<string>;  // Тип "Да, это строка"
type B = IsString<number>;  // Тип "Нет, не строка"
```
- **Union/Intersection**
	 
	- `Union` - объединение множеств `|`
	- `Intersection` - Пересечение множеств `&`
``` TypeScript
// Union |
// Example 1 (Primitives)
let data: number | string; // <- number ИЛИ string
data = 5;
data = "str";

let color 'red' | 'blue';

// Example 2 (Objects)
type MainInfo = {
	firstname: string;
	lastname: string;
}

type AdditionalInfo = {
	age: number;
}

type FullInfo = MainInfo | AdditionalInfo;
```
	
``` TypeScript
// Intersection &
// Example 3 (Objects)
type MainInfo = {
	firstname: string;
	lastname: string;
}

type AdditionalInfo = {
	age: number;
}

type FullInfo = MainInfo & AdditionalInfo; // <- Должны быть поля И MainInfo И AdditionalInfo 
```
- **Надтип/Подтип**
	
	- `SuperType` - Надтип может содержать меньше свойств и/или методов, чем подтип
	- `SubType` - Подтип включает в себя все свойства и/или методы надтипа + может добавлять свои
``` TypeScript
type SuperType = {
	name: string;
}

type SubType = {
	name: string;
	age: number;
}

// Example 1 (Correct)
const subType: SubType = { name: "Amir", age: 20 };
const superType: SuperType = subType;

// Example 2 (Incorrect)
const superType2: SuperType = { name: "Arthur" };
const subType2: SubType = superType2;
```

> Как мыслить о типах? - Нужно воспринимать типы в качестве множества, они могут быть как надтипом, так и подтипом. С ними можно проводить различные операции множеств.

