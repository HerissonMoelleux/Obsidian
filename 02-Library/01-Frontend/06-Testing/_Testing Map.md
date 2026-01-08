# Testing Map

> Тесты — не опция, а требование. Без них не возьмут на нормальную работу.

---

## 🎯 Почему эта папка существует?

**Тесты — требование для Junior+.** Без них:
- Не возьмут на нормальную работу
- Не дадут мержить PR без тестов
- Страшно рефакторить код

**Аналогия:** Тесты перед выпуском продукта. Автомобиль без crash-тестов никто не купит.

---

## 📁 Structure

```
06-Testing/
├── Fundamentals/
│   ├── Test Types.md             # Unit, integration, e2e
│   ├── AAA Pattern.md            # Arrange, Act, Assert
│   ├── What to Test.md           # ⭐ Частый вопрос новичков
│   └── Mocking Concepts.md       # Why & when to mock
│
├── Vitest/
│   ├── Setup.md                  # Installation, config
│   ├── Test Structure.md         # describe, it, test
│   ├── Matchers.md               # toBe, toEqual, toThrow
│   ├── Async Tests.md            # Testing promises
│   └── Mocking.md                # vi.fn, vi.mock, vi.spyOn
│
├── React Testing Library/
│   ├── Philosophy.md             # Test behavior, not implementation
│   ├── Queries.md                # getBy, queryBy, findBy
│   ├── User Events.md            # userEvent.click, type
│   ├── Async Testing.md          # waitFor, findBy
│   └── Testing Hooks.md          # renderHook
│
└── Patterns/
    ├── MSW.md                    # ⭐ Mock Service Worker
    ├── Test Organization.md      # File structure, naming
    └── Component Testing.md      # Common patterns
```

---

## 📚 Fundamentals

Базовые концепции тестирования.

### Topics
- [[Test Types]] — unit, integration, e2e
- [[AAA Pattern]] — Arrange, Act, Assert
- [[Test Pyramid]] — сколько каких тестов писать
- [[Mocking]] — зачем и когда мокать
- [[Test Coverage]] — метрики и их смысл
- [[TDD Basics]] — test-driven development

### 💡 Test Pyramid
```
        /\
       /  \      E2E (few)
      /----\     
     /      \    Integration (some)
    /--------\   
   /          \  Unit (many)
  /----------->\
```

### Key Questions (Interview)
- Разница между unit и integration тестами?
- Что такое mocking и когда использовать?
- Как понять что тестировать?

---

## ⚡ Vitest

Быстрый test runner для Vite проектов.

### Topics
- [[Vitest Setup]] — установка, конфигурация
- [[Test Structure]] — describe, it, test
- [[Matchers]] — toBe, toEqual, toThrow, etc.
- [[Async Testing]] — async/await в тестах
- [[Mocking in Vitest]] — vi.fn(), vi.mock(), vi.spyOn()
- [[Setup and Teardown]] — beforeEach, afterEach

### 💡 Basic Test Structure
```typescript
import { describe, it, expect, vi } from 'vitest';

describe('Calculator', () => {
  it('should add two numbers', () => {
    // Arrange
    const a = 2;
    const b = 3;
    
    // Act
    const result = add(a, b);
    
    // Assert
    expect(result).toBe(5);
  });
});
```

### 💡 Mocking
```typescript
// Mock function
const mockFn = vi.fn();
mockFn.mockReturnValue(42);

// Mock module
vi.mock('./api', () => ({
  fetchUsers: vi.fn().mockResolvedValue([{ id: 1, name: 'John' }]),
}));

// Spy on method
const spy = vi.spyOn(console, 'log');
```

---

## 🧪 React Testing Library

Тестирование React-компонентов "как пользователь".

### Topics
- [[RTL Philosophy]] — test behavior, not implementation
- [[Queries]] — getBy, queryBy, findBy
- [[User Events]] — userEvent.click, type, etc.
- [[Async Testing RTL]] — waitFor, findBy queries
- [[Testing Hooks]] — renderHook
- [[Testing Forms]] — input, submit, validation

### 💡 Query Priority
```typescript
// ✅ Accessible queries (prefer these)
getByRole('button', { name: /submit/i })
getByLabelText('Email')
getByPlaceholderText('Enter email')
getByText('Welcome')

// ⚠️ Semantic queries
getByAltText('Profile photo')
getByTitle('Close')

// ❌ Test IDs (last resort)
getByTestId('submit-button')
```

### 💡 Component Test Example
```typescript
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';

describe('LoginForm', () => {
  it('should submit form with valid data', async () => {
    const user = userEvent.setup();
    const onSubmit = vi.fn();
    
    render(<LoginForm onSubmit={onSubmit} />);
    
    await user.type(screen.getByLabelText(/email/i), 'test@example.com');
    await user.type(screen.getByLabelText(/password/i), 'password123');
    await user.click(screen.getByRole('button', { name: /submit/i }));
    
    expect(onSubmit).toHaveBeenCalledWith({
      email: 'test@example.com',
      password: 'password123',
    });
  });
});
```

### Key Questions (Interview)
- Почему getByRole лучше getByTestId?
- Как тестировать async компоненты?
- Что такое userEvent vs fireEvent?

---

## 🎨 Patterns

Паттерны и best practices.

### Topics
- [[What to Test]] — что тестировать, а что нет
- [[Test Organization]] — структура файлов, naming
- [[MSW (Mock Service Worker)]] — мокирование API
- [[Testing Custom Hooks]] — renderHook patterns
- [[Snapshot Testing]] — когда полезно
- [[Testing Error States]] — error boundaries, fallbacks

### 💡 MSW Example
```typescript
import { setupServer } from 'msw/node';
import { http, HttpResponse } from 'msw';

const server = setupServer(
  http.get('/api/users', () => {
    return HttpResponse.json([
      { id: 1, name: 'John' },
      { id: 2, name: 'Jane' },
    ]);
  })
);

beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());
```

### What to Test (Priority)
```
1. User interactions — клики, ввод, навигация
2. Conditional rendering — что показывается когда
3. API integration — loading, success, error states
4. Edge cases — пустые данные, ошибки
5. Accessibility — роли, labels
```

### What NOT to Test
```
- Implementation details (internal state)
- Third-party libraries
- CSS styling
- Static content that doesn't change
```

---

## 🔗 Connections

- [[_React Map]] — тестирование React-компонентов
- [[_Data Fetching Map]] — MSW для API мокирования
- [[_TypeScript Map]] — типизация тестов

---

## 📈 Progress

### Must Know (Junior)
- [ ] Test types (unit, integration)
- [ ] Vitest basics
- [ ] Simple component tests
- [ ] AAA pattern

### Must Know (Junior+)
- [ ] RTL queries & userEvent
- [ ] Async testing
- [ ] Mocking (vi.fn, vi.mock)
- [ ] MSW basics
- [ ] Testing hooks

### Good to Know
- [ ] E2E with Playwright/Cypress
- [ ] Coverage analysis
- [ ] TDD approach

---

*Part of [[_Frontend Development Map]]*
