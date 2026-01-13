# TypeScript: Заметки по видео-лекции

## План лекции

- **Самое главное:** научиться понимать, а не писать код интуитивно по заученным шаблонам.
- Проблемы JavaScript, вид типизации, как устроена работа с примитивами и объектами, хранение в памяти.
- Что представляет из себя TypeScript? Что такое яваная/неявная, статическая и структурная типизация?
- Как воспринимать типы? Работа с множествами.
- Поделим типы на подгруппы и разберемся с каждой.
- Разберем понятия супертип и надтип.
- `never`, `unknown`, `any`, `void` - в концепции супертипов и надтипов. Учимся действительно понимать, как они устроены.
- Разберем дженерики и условные типы.
- Рассмотрим концепцию сужения и расширения типов, и то какими способами этого можно добиться.
- Поговорим о преобразовании типов, хорошие и плохие практики. Рассмотрим опасные примеры.
- Рассмотрим различные операторы.
- `Infer` и как его понять и начать готовить.
- Конфигурация проекта и пример большого эталонного проекта.


## Проблематика

- **JavaScript - язык со слабой динамической типизацией**
	
	- Слабая типизация JavaScript позволяет работать с разными типами данных, при этом неявно преобразуя их ([[Coercion]]).
	- Динамическая типизация определяет тип в `runtime` т.е. во время выполнения программы, а не на этапе компиляции и написания кода.

- Сложность в поддержке больших проектов (много данных, нет четкого описания)
- На этапе написания кода отлиавливать проблемы с типами приходится в уме
- Усложняется дебаг и тестирование кода
- Усложняется анализ кода разработчиком. Требуется дополнительная когнитивная нагрузка для анализа кода
- Отсутствие адекватного автокомплита в среде разработки

## TypeScript

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
- **Составные типы**
- **Специальные типы**
	- 
- **Литералы**
- **Generic types**
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
Как мыслить о типах? - Нужно воспринимать типы в качестве множества, они могут быть как надтипом, так и подтипом. С ними можно проводить различные операции множеств.

