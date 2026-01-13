# 🎯 2-Week Intensive Frontend Development Plan

**Goal:** Close critical gaps in async JavaScript, TypeScript basics, and debugging skills  
**Duration:** 14 days  
**Daily commitment:** 3-4 hours  
**Format:** Theory → Practice → Build

---

## 📋 Overview

### Week 1 Focus: Async JavaScript + Debugging Tools

- Days 1-3: Promises, fetch, async/await
- Days 4-5: Error handling, loading states
- Days 6-7: Practice projects + React DevTools

### Week 2 Focus: TypeScript Basics + Integration

- Days 8-10: TypeScript fundamentals
- Days 11-12: TypeScript + React
- Days 13-14: Mini-project with everything combined

---

## 🗓️ WEEK 1: Async JavaScript Mastery

### Day 1: Promises Fundamentals

**Time: 3 hours**

#### Morning (1.5h): Theory

- [x] Read: [JavaScript.info - Promises](https://javascript.info/promise-basics)
- [x] Watch: [Promises in 10 minutes](https://www.youtube.com/watch?v=DHvZLI7Db8E) (Web Dev Simplified)
- [x] Understand: Promise states (pending/fulfilled/rejected)

**На простом языке:** Сегодня разбираешься, как работают Promise под капотом.

#### Afternoon (1.5h): Practice

```javascript
// Task 1: Создай Promise вручную
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Success!");
  }, 1000);
});

// Task 2: Promise chain
myPromise
  .then(result => console.log(result))
  .catch(error => console.log(error));

// Task 3: Напиши функцию delay(ms)
function delay(ms) {
  // Возвращает Promise, который resolve через ms миллисекунд
  return new Promise ((resolve) => {
    setTimeout(resolve, ms)
  })
}

// Использование:
delay(2000).then(() => console.log("2 seconds passed"));
```

**Deliverable:** 5-7 небольших функций с Promise

---

### Day 2: Fetch API & HTTP Requests

**Time: 3.5 hours**

#### Morning (1.5h): Theory

- [x] Read: [MDN - Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- [x] Understand: HTTP methods (GET, POST, PUT, DELETE)
- [x] Learn: Response object (.json(), .text(), .status)

#### Afternoon (2h): Practice with Public API

```javascript
// Task 1: Fetch users list
fetch('https://jsonplaceholder.typicode.com/users')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));

// Task 2: Fetch single user by ID
// Task 3: Create a new post (POST request)
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ title: 'My Post', body: 'Content', userId: 1 })
})
  .then(res => res.json())
  .then(data => console.log(data));
```

**Deliverable:** 10 разных fetch запросов (GET, POST, PUT, DELETE)

---

### Day 3: Async/Await Syntax

**Time: 3 hours**

#### Morning (1h): Theory

- [x] Read: [JavaScript.info - Async/Await](https://javascript.info/async-await)
- [x] Understand: Why async/await is better than .then()
- [x] Learn: Error handling with try/catch

#### Afternoon (2h): Rewrite Yesterday's Code

```javascript
// OLD WAY (.then)
fetch('https://jsonplaceholder.typicode.com/users')
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));

// NEW WAY (async/await)
async function getUsers() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

getUsers();
```

**Task:** Переписать ВСЕ вчерашние fetch запросы на async/await

**Deliverable:** Файл с 10 функциями (async/await style)

---

### Day 4: React + Async (Loading States)

**Time: 4 hours**

#### Morning (2h): Create Basic Component

```javascript
import { useState, useEffect } from 'react';

function UsersList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchUsers() {
      setLoading(true);
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users');
        const data = await response.json();
        setUsers(data);
      } catch (error) {
        console.error(error);
      } finally {
        setLoading(false);
      }
    }
    
    fetchUsers();
  }, []);

  if (loading) return <p>Loading...</p>;

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

#### Afternoon (2h): Add Features

- [ ] Task 1: Add error state
- [ ] Task 2: Add "Retry" button on error
- [ ] Task 3: Add search filter

**Deliverable:** Working React component with loading/error states

---

### Day 5: Error Handling Patterns

**Time: 3.5 hours**

#### Morning (1.5h): Learn Error Types

```javascript
// 1. Network errors
try {
  const res = await fetch('https://invalid-url.com');
} catch (error) {
  console.log('Network error:', error);
}

// 2. HTTP errors (404, 500)
const response = await fetch('https://jsonplaceholder.typicode.com/users/999999');
if (!response.ok) {
  throw new Error(`HTTP error! status: ${response.status}`);
}

// 3. JSON parsing errors
try {
  const data = await response.json();
} catch (error) {
  console.log('Invalid JSON');
}
```

#### Afternoon (2h): Build Robust Fetcher

```javascript
async function robustFetch(url) {
  try {
    const response = await fetch(url);
    
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }
    
    const data = await response.json();
    return { data, error: null };
    
  } catch (error) {
    return { data: null, error: error.message };
  }
}

// Usage in React
const { data, error } = await robustFetch('/api/users');
if (error) {
  setError(error);
} else {
  setUsers(data);
}
```

**Deliverable:** Reusable fetch wrapper function + React component using it

---

### Day 6: React DevTools + Debugging

**Time: 3 hours**

#### Morning (1h): Setup & Learn

- [ ] Install: [React DevTools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
- [ ] Watch: [React DevTools Tutorial](https://www.youtube.com/watch?v=rb1GWqCJid4) (15 min)
- [ ] Practice: Inspect your components, view props/state

#### Afternoon (2h): Debugging Practice

```javascript
// Создай компонент с багом:
function BuggyComponent() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    setCount(count + 1); // ❌ Бесконечный цикл! Почему?
  }, [count]);
  
  return <div>{count}</div>;
}

// Tasks:
// 1. Найди баг через React DevTools (смотри на renders)
// 2. Исправь
// 3. Создай ещё 3 компонента с разными багами
// 4. Научись находить их через DevTools
```

**Deliverable:** Document (md файл) с 5 типичными багами и как их найти в DevTools

---

### Day 7: Practice Project - Weather App

**Time: 4-5 hours**

#### Full Day: Build Complete App

**Requirements:**

```javascript
// API: OpenWeatherMap (бесплатный)
// https://api.openweathermap.org/data/2.5/weather?q=London&appid=YOUR_API_KEY

// Features:
1. Input для города
2. Кнопка "Search"
3. Loading state при запросе
4. Error handling (город не найден)
5. Показывать: температуру, описание, иконку погоды
6. Styled components (CSS или inline styles)
```

**Component Structure:**

```
App
├── SearchBar (input + button)
├── WeatherDisplay (shows data)
└── ErrorMessage (shows errors)
```

**Deliverable:** Working weather app deployed on Vercel/Netlify

**Bonus:** Add "Recent Searches" list (localStorage)

---

## 🗓️ WEEK 2: TypeScript Integration

### Day 8: TypeScript Basics

**Time: 3 hours**

#### Morning (1.5h): Core Concepts

- [ ] Read: [TypeScript Handbook - Basics](https://www.typescriptlang.org/docs/handbook/2/basic-types.html)
- [ ] Learn: Primitives (string, number, boolean)
- [ ] Learn: Arrays, Objects, Functions

```typescript
// Primitives
let name: string = "Alice";
let age: number = 25;
let isActive: boolean = true;

// Arrays
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ["Alice", "Bob"];

// Objects
let user: { name: string; age: number } = {
  name: "Alice",
  age: 25
};

// Functions
function greet(name: string): string {
  return `Hello, ${name}`;
}
```

#### Afternoon (1.5h): Practice

- [ ] Создай TypeScript playground на [TypeScript Playground](https://www.typescriptlang.org/play)
- [ ] Напиши 20 функций с типами
- [ ] Все функции из Day 1-3 переписать с типами

**Deliverable:** 20 typed functions

---

### Day 9: TypeScript - Interfaces & Types

**Time: 3.5 hours**

#### Morning (1.5h): Theory

```typescript
// Type Alias
type User = {
  id: number;
  name: string;
  email: string;
  age?: number; // optional
};

// Interface (similar, but can be extended)
interface Product {
  id: number;
  title: string;
  price: number;
}

// Union Types
type Status = "loading" | "success" | "error";

// Extending
interface ExtendedUser extends User {
  role: "admin" | "user";
}
```

#### Afternoon (2h): Practice

```typescript
// Task 1: Create types for your weather app
type WeatherData = {
  // определи структуру
};

type ApiResponse<T> = {
  data: T | null;
  error: string | null;
  loading: boolean;
};

// Task 2: Type your fetch functions
async function fetchWeather(city: string): Promise<WeatherData> {
  // implementation
}
```

**Deliverable:** Typed versions of all Day 1-7 code

---

### Day 10: Generics & Utility Types

**Time: 3 hours**

#### Morning (1h): Generics

```typescript
// Generic function
function identity<T>(arg: T): T {
  return arg;
}

identity<string>("hello"); // T = string
identity<number>(42);      // T = number

// Generic interface
interface ApiResponse<T> {
  data: T;
  status: number;
}

const userResponse: ApiResponse<User> = {
  data: { id: 1, name: "Alice" },
  status: 200
};
```

#### Afternoon (2h): Utility Types

```typescript
// Built-in utility types

// 1. Partial (все поля optional)
type User = { name: string; age: number };
type PartialUser = Partial<User>; // { name?: string; age?: number }

// 2. Pick (выбрать определённые поля)
type UserPreview = Pick<User, "name">; // { name: string }

// 3. Omit (исключить поля)
type UserWithoutAge = Omit<User, "age">; // { name: string }

// 4. Required (все поля обязательные)
type RequiredUser = Required<PartialUser>;
```

**Practice:**

- [ ] Создай 10 разных типов с generics
- [ ] Используй каждый utility type в реальном примере

**Deliverable:** Cheat sheet (md) с примерами всех utility types

---

### Day 11: TypeScript + React (Props & State)

**Time: 4 hours**

#### Morning (2h): Setup & Basic Types

```bash
# Создай новый React + TS проект
npm create vite@latest my-ts-app -- --template react-ts
cd my-ts-app
npm install
npm run dev
```

```typescript
// Component with typed props
interface ButtonProps {
  label: string;
  onClick: () => void;
  disabled?: boolean;
}

function Button({ label, onClick, disabled = false }: ButtonProps) {
  return (
    <button onClick={onClick} disabled={disabled}>
      {label}
    </button>
  );
}

// Component with typed state
function Counter() {
  const [count, setCount] = useState<number>(0);
  // TypeScript знает, что count - это number
  
  return <div>{count}</div>;
}
```

#### Afternoon (2h): Complex Types

```typescript
// Event handlers
function handleChange(event: React.ChangeEvent<HTMLInputElement>) {
  console.log(event.target.value);
}

function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
  event.preventDefault();
}

// Children prop
interface CardProps {
  title: string;
  children: React.ReactNode;
}

function Card({ title, children }: CardProps) {
  return (
    <div>
      <h2>{title}</h2>
      {children}
    </div>
  );
}
```

**Deliverable:** Convert Day 4 UsersList component to TypeScript

---

### Day 12: TypeScript + Async React

**Time: 4 hours**

#### Full Day: Type Everything

**Task:** Convert your Weather App (Day 7) to TypeScript

```typescript
// Types to create:
type Weather = {
  temp: number;
  description: string;
  icon: string;
};

type WeatherResponse = {
  main: {
    temp: number;
  };
  weather: Array<{
    description: string;
    icon: string;
  }>;
};

type AppState = {
  weather: Weather | null;
  loading: boolean;
  error: string | null;
};

// Typed API function
async function fetchWeather(city: string): Promise<WeatherResponse> {
  const response = await fetch(`API_URL?q=${city}`);
  if (!response.ok) {
    throw new Error('City not found');
  }
  return response.json();
}

// Typed component
function WeatherApp() {
  const [state, setState] = useState<AppState>({
    weather: null,
    loading: false,
    error: null
  });
  
  // ...
}
```

**Deliverable:** Fully typed Weather App with 0 TypeScript errors

---

### Day 13-14: Final Project - TODO App with API

**Time: 8-10 hours (split across 2 days)**

#### Requirements:

**API:** [JSONPlaceholder Todos](https://jsonplaceholder.typicode.com/todos)

**Features:**

1. ✅ Fetch todos from API
2. ✅ Display todos list
3. ✅ Add new todo (POST)
4. ✅ Toggle complete status (PATCH)
5. ✅ Delete todo (DELETE)
6. ✅ Filter: All / Active / Completed
7. ✅ Loading states
8. ✅ Error handling
9. ✅ TypeScript (strict mode)
10. ✅ React DevTools inspection

**TypeScript Types:**

```typescript
interface Todo {
  id: number;
  title: string;
  completed: boolean;
  userId: number;
}

type FilterType = "all" | "active" | "completed";

interface AppState {
  todos: Todo[];
  filter: FilterType;
  loading: boolean;
  error: string | null;
}
```

**Component Structure:**

```
App (AppState)
├── TodoInput (add new)
├── FilterButtons (change filter)
├── TodoList
│   └── TodoItem (toggle, delete)
└── ErrorMessage
```

**Day 13:** Build all components + API integration  
**Day 14:** Polish, add styles, test all edge cases, deploy

**Deliverable:**

- GitHub repo with clean code
- Deployed app (Vercel/Netlify)
- README with screenshots
