# TypeScript Map

> JavaScript с типами. Твой щит от багов и друг на code review.

---

## 🎯 Почему эта папка существует?

TypeScript — **обязательное требование** на 90% вакансий React. Это не "nice to have", это must have.

**Преимущества:**
1. **Catch bugs early** — ошибки видны до запуска
2. **Better DX** — автокомплит, рефакторинг, документация в коде
3. **Required for jobs** — 90%+ вакансий React требуют TS
4. **Self-documenting** — типы = документация

---

## 📁 Structure

```
03-TypeScript/
├── Basics/
│   ├── Primitive Types.md        # string, number, boolean, null, undefined
│   ├── Arrays and Tuples.md      # string[], [string, number]
│   ├── Interfaces.md             # Interface declaration, extending
│   ├── Type Aliases.md           # type keyword, когда что использовать
│   ├── Union Types.md            # |, literal types
│   └── Type Inference.md         # Когда TS понимает тип сам
│
├── Advanced Types/
│   ├── Generics.md               # ⭐ <T>, constraints — must know
│   ├── Utility Types.md          # Partial, Pick, Omit, Record
│   ├── Conditional Types.md      # T extends U ? X : Y
│   ├── Mapped Types.md           # { [K in keyof T]: ... }
│   └── Type Narrowing.md         # Type guards, discrimination
│
├── Configuration/
│   ├── tsconfig.md               # Основные опции
│   └── Strict Mode.md            # Что включает strict: true
│
└── Patterns/
    ├── Type Guards.md            # typeof, instanceof, custom
    ├── Discriminated Unions.md   # ⭐ Очень полезно для state
    └── Branded Types.md          # Nominal typing
```

### Связь с React
Большинство TS-знаний ты будешь применять **внутри React**:
- Typing props → `Basics/Interfaces.md`
- Typing hooks → `Advanced Types/Generics.md`
- Typing events → создай кросс-ссылку с React

---

## 📝 Basics

Фундамент типизации.

### Topics
- [[Primitive Types]] — string, number, boolean, null, undefined
- [[Arrays and Tuples]] — `string[]`, `Array<string>`, `[string, number]`
- [[Objects and Interfaces]] — object types, interface declaration
- [[Type Aliases]] — `type` keyword, когда использовать
- [[Union and Intersection]] — `|` и `&` операторы
- [[Literal Types]] — `"success" | "error"`, const assertions
- [[Type Inference]] — когда TS сам понимает тип

### Key Questions (Interview)
- Разница между `interface` и `type`?
- Когда использовать `unknown` vs `any`?
- Что такое literal types?

### 💡 Interface vs Type
```typescript
// Interface — для объектов, можно extend
interface User {
  name: string;
  age: number;
}

// Type — для всего, включая unions
type Status = "loading" | "success" | "error";
type UserWithStatus = User & { status: Status };
```

---

## 🔬 Advanced Types

Мощь TypeScript — в системе типов.

### Topics
- [[Generics]] — `<T>`, constraints, default types
- [[Utility Types]] — Partial, Required, Pick, Omit, Record
- [[Conditional Types]] — `T extends U ? X : Y`
- [[Mapped Types]] — `{ [K in keyof T]: ... }`
- [[Template Literal Types]] — типы из строк
- [[Type Narrowing]] — сужение типов через проверки

### Key Questions (Interview)
- Как работают generics? Приведи пример.
- Объясни `Partial<T>` и `Pick<T, K>`
- Что такое type narrowing?

### 💡 Generics Example
```typescript
// Generic function
function getFirst<T>(arr: T[]): T | undefined {
  return arr[0];
}

// Generic with constraint
function getLength<T extends { length: number }>(item: T): number {
  return item.length;
}
```

---

## ⚙️ Configuration

Настройка TypeScript проекта.

### Topics
- [[tsconfig.json]] — основные опции
- [[Strict Mode]] — что включает strict: true
- [[Compiler Options]] — target, module, moduleResolution
- [[Path Aliases]] — `@/components/*` вместо `../../../`

### Key Settings
```json
{
  "compilerOptions": {
    "strict": true,           // ВСЕГДА включай
    "noImplicitAny": true,    // Часть strict
    "strictNullChecks": true, // Часть strict
    "esModuleInterop": true,  // Совместимость импортов
    "skipLibCheck": true      // Быстрее компиляция
  }
}
```

---

## 🎨 Patterns

Паттерны использования TypeScript.

### Topics
- [[Type Guards]] — `typeof`, `instanceof`, custom guards
- [[Discriminated Unions]] — tagged unions для state
- [[Branded Types]] — номинальная типизация
- [[Function Overloads]] — разные сигнатуры функции
- [[Assertion Functions]] — `asserts condition`

### 💡 Discriminated Union (часто используется!)
```typescript
type State = 
  | { status: "loading" }
  | { status: "success"; data: User[] }
  | { status: "error"; error: string };

function handleState(state: State) {
  switch (state.status) {
    case "loading":
      return <Spinner />;
    case "success":
      return <UserList users={state.data} />; // TS знает про data!
    case "error":
      return <Error message={state.error} />; // TS знает про error!
  }
}
```

---

## 🔗 Connections

- [[_JavaScript Map]] — TS = JS + types
- [[_React Map]] — React + TypeScript integration
- [[_Testing Map]] — типы помогают писать тесты

---

## 🔐 Security Angle

> TypeScript помогает безопасности:
> - Строгая типизация предотвращает инъекции
> - Zod + TS = runtime + compile-time validation
> - `unknown` вместо `any` для внешних данных

---

## 📈 Progress

### Must Know (Junior)
- [ ] Primitive types & arrays
- [ ] Interfaces & type aliases
- [ ] Union types
- [ ] Basic generics
- [ ] Type inference

### Must Know (Junior+)
- [ ] Utility types (Partial, Pick, Omit)
- [ ] Type guards & narrowing
- [ ] Discriminated unions
- [ ] Generic constraints
- [ ] tsconfig strict mode

### Good to Know
- [ ] Conditional types
- [ ] Mapped types
- [ ] Template literal types

---

## 🎯 Practice Projects

1. **Type a REST API response** — типизируй данные с JSONPlaceholder
2. **Create utility types** — напиши свои Partial, Required
3. **React + TS** — типизируй props, events, hooks

---

*Part of [[_Frontend Development Map]]*
