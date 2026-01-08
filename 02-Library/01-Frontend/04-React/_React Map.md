# React Map

> UI-библиотека, которая изменила фронтенд. Твой главный инструмент.

---

## 🎯 Почему эта папка существует?

Это **твой главный рабочий инструмент**. React-папка будет самой большой и самой часто обновляемой.

**Аналогия:** Кисти для художника. Можно знать теорию цвета, но без владения кистью картины не будет.

---

## 📁 Structure

```
04-React/
├── Core/
│   ├── Components.md             # Functional components, composition
│   ├── JSX.md                    # Syntax, expressions, compilation
│   ├── Props.md                  # Passing data, children, spread
│   ├── Rendering.md              # When & why re-renders happen
│   └── Lists and Keys.md         # Why key matters
│
├── Hooks/
│   ├── useState.md               # Local state
│   ├── useEffect.md              # ⭐ Side effects, cleanup, deps
│   ├── useRef.md                 # Mutable values, DOM refs
│   ├── useContext.md             # Context consumption
│   ├── useMemo.md                # Memoizing computations
│   ├── useCallback.md            # Memoizing functions
│   ├── useReducer.md             # Complex state logic
│   └── Custom Hooks.md           # ⭐ Creating your own hooks
│
├── State Management/
│   ├── Lifting State Up.md       # Shared state pattern
│   ├── Context API.md            # Built-in global state
│   ├── Zustand.md                # ⭐ Simple state manager
│   └── When to Use What.md       # Decision guide
│
├── Routing/
│   ├── React Router Setup.md     # BrowserRouter, Routes
│   ├── Navigation.md             # Link, useNavigate
│   ├── Route Parameters.md       # useParams, dynamic routes
│   └── Protected Routes.md       # Auth guards
│
├── Forms/
│   ├── Controlled Components.md  # value + onChange
│   ├── React Hook Form.md        # ⭐ Form library
│   └── Zod Integration.md        # Validation
│
├── Styling/
│   ├── CSS Modules.md            # Scoped styles
│   └── Tailwind in React.md      # Utility-first approach
│
├── Performance/
│   ├── React.memo.md             # Component memoization
│   ├── Code Splitting.md         # React.lazy, Suspense
│   └── When to Optimize.md       # Avoid premature optimization
│
├── Patterns/
│   ├── Composition Pattern.md    # ⭐ Instead of inheritance
│   ├── Custom Hooks Pattern.md   # Extracting logic
│   └── Compound Components.md    # Related components
│
└── Internals/
    ├── Virtual DOM.md            # What & why
    ├── Reconciliation.md         # Diffing algorithm
    └── Fiber.md                  # Modern React engine
```

### Особенность этой папки
React — это **экосистема**. Многие темы пересекаются:
- `Forms/Zod Integration.md` связана с `[[TypeScript/Patterns/Type Guards]]`
- `Hooks/useEffect.md` связана с `[[JavaScript/Async/Event Loop]]`

Используй `[[wiki-links]]` активно!

---

## 🧱 Core

Фундамент React.

### Topics
- [[Components]] — функциональные компоненты, композиция
- [[JSX]] — синтаксис, expressions, conditional rendering
- [[Props]] — передача данных, children, spread props
- [[Rendering]] — когда и почему компонент перерендеривается
- [[Lists and Keys]] — рендеринг списков, почему key важен

### Key Questions (Interview)
- Что такое JSX и во что он компилируется?
- Зачем нужен key в списках?
- Когда компонент перерендеривается?

---

## 🪝 Hooks

Хуки — сердце современного React.

### Topics
- [[useState]] — локальное состояние
- [[useEffect]] — side effects, cleanup, dependencies
- [[useRef]] — мутабельные значения, DOM-ссылки
- [[useContext]] — доступ к контексту
- [[useMemo]] — мемоизация вычислений
- [[useCallback]] — мемоизация функций
- [[useReducer]] — complex state logic
- [[Custom Hooks]] — создание своих хуков

### Key Questions (Interview)
- Как работает useEffect? Что такое cleanup?
- Разница между useMemo и useCallback?
- Когда стоит создавать custom hook?

### 💡 useEffect Pattern
```typescript
useEffect(() => {
  // Effect logic
  const subscription = api.subscribe(id);
  
  // Cleanup (важно!)
  return () => {
    subscription.unsubscribe();
  };
}, [id]); // Dependencies
```

### ⚠️ Common Gotchas
- Забытые зависимости в useEffect
- Бесконечные циклы при неправильных deps
- Использование useMemo/useCallback везде (premature optimization)

---

## 🗃️ State Management

Управление состоянием приложения.

### Topics
- [[Lifting State Up]] — поднятие состояния к общему предку
- [[Context API]] — глобальное состояние без prop drilling
- [[Zustand]] — простой и мощный state manager
- [[When to Use What]] — локальный vs глобальный state

### Key Questions (Interview)
- Когда использовать Context vs Zustand?
- Что такое prop drilling и как избежать?

### 💡 Zustand Example
```typescript
import { create } from 'zustand';

interface CounterStore {
  count: number;
  increment: () => void;
  decrement: () => void;
}

const useCounter = create<CounterStore>((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
  decrement: () => set((state) => ({ count: state.count - 1 })),
}));
```

---

## 🧭 Routing

Навигация в SPA.

### Topics
- [[React Router Setup]] — BrowserRouter, Routes, Route
- [[Navigation]] — Link, useNavigate, useLocation
- [[Route Parameters]] — useParams, dynamic routes
- [[Protected Routes]] — auth guards, redirects
- [[Nested Routes]] — layouts, Outlet

### Key Questions (Interview)
- Как сделать protected route?
- Разница между `<Link>` и `useNavigate`?

---

## 📝 Forms

Работа с формами — частая задача.

### Topics
- [[Controlled Components]] — value + onChange
- [[React Hook Form]] — performant forms library
- [[Zod Integration]] — validation с типами
- [[Form Patterns]] — multi-step, dynamic fields

### 💡 React Hook Form + Zod
```typescript
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { z } from 'zod';

const schema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
});

type FormData = z.infer<typeof schema>;

const { register, handleSubmit, formState: { errors } } = useForm<FormData>({
  resolver: zodResolver(schema),
});
```

### 🔐 Security Angle
> Zod даёт runtime validation — защита от malicious input.
> Всегда валидируй на клиенте И на сервере.

---

## 🎨 Styling

Стилизация компонентов.

### Topics
- [[CSS Modules]] — scoped styles, className
- [[Tailwind CSS]] — utility-first подход
- [[CSS-in-JS]] — styled-components, Emotion (обзор)
- [[Styling Patterns]] — variants, conditional styles

---

## ⚡ Performance

Оптимизация React-приложений.

### Topics
- [[React.memo]] — мемоизация компонентов
- [[useMemo and useCallback]] — когда реально нужны
- [[Code Splitting]] — React.lazy, Suspense
- [[Virtualization]] — react-window для длинных списков
- [[Profiler]] — инструменты анализа производительности

### Key Questions (Interview)
- Когда использовать React.memo?
- Как работает code splitting?

---

## 🏗️ Patterns

Архитектурные паттерны React.

### Topics
- [[Composition Pattern]] — вместо наследования
- [[Custom Hooks Pattern]] — извлечение логики
- [[Compound Components]] — связанные компоненты
- [[Render Props]] — (legacy, но спрашивают)
- [[Container-Presentational]] — разделение логики и UI

### 💡 Composition Example
```typescript
// ❌ Prop drilling
<Card
  title="..."
  subtitle="..."
  icon={<Icon />}
  footer={<Button />}
/>

// ✅ Composition
<Card>
  <Card.Header>
    <Icon />
    <Card.Title>...</Card.Title>
  </Card.Header>
  <Card.Footer>
    <Button />
  </Card.Footer>
</Card>
```

---

## 🔬 Internals

Как React работает под капотом.

### Topics
- [[Virtual DOM]] — что это и зачем
- [[Reconciliation]] — алгоритм сравнения
- [[Fiber Architecture]] — современный движок React
- [[Batching]] — группировка обновлений

### Key Questions (Interview)
- Что такое Virtual DOM и какую проблему решает?
- Как работает reconciliation?

---

## 🔗 Connections

- [[_JavaScript Map]] — React = JavaScript + JSX
- [[_TypeScript Map]] — типизация React-компонентов
- [[_Data Fetching Map]] — загрузка данных в React
- [[_Testing Map]] — тестирование React-компонентов

---

## 📈 Progress

### Must Know (Junior)
- [ ] Components & Props
- [ ] useState & useEffect
- [ ] Lists & Keys
- [ ] Basic routing
- [ ] Controlled forms

### Must Know (Junior+)
- [ ] All major hooks
- [ ] Custom hooks
- [ ] Zustand
- [ ] React Hook Form + Zod
- [ ] Performance basics (memo, lazy)
- [ ] Common patterns

### Good to Know
- [ ] Internals (Fiber, Reconciliation)
- [ ] Advanced patterns
- [ ] Compound components

---

*Part of [[_Frontend Development Map]]*
