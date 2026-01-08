# Data Fetching Map

> Связь фронтенда с бэкендом. Без этого приложение — просто красивая картинка.

---

## 🎯 Почему эта папка существует отдельно?

Работа с серверными данными — **отдельная большая тема**:
- Свои паттерны (loading, error, success states)
- Свои библиотеки (TanStack Query)
- Свои проблемы (race conditions, caching)

Можно было бы положить в React, но тогда React-папка станет огромной.

**Аналогия:** Телефон для общения. React — это ты, сервер — собеседник, Data Fetching — связь между вами.

---

## 📁 Structure

```
05-Data Fetching/
├── Fundamentals/
│   ├── Fetch API.md              # Native browser API
│   ├── Axios.md                  # Popular library, interceptors
│   ├── HTTP Methods.md           # GET, POST, PUT, DELETE in practice
│   └── Error Handling.md         # HTTP vs network errors
│
├── React Integration/
│   ├── useEffect Fetching.md     # Classic pattern
│   ├── Custom Fetch Hook.md      # useFetch abstraction
│   ├── Loading States.md         # loading, error, data pattern
│   └── Race Conditions.md        # ⭐ AbortController, cleanup
│
├── TanStack Query/
│   ├── Query Basics.md           # useQuery fundamentals
│   ├── Mutations.md              # useMutation, onSuccess
│   ├── Invalidation.md           # When & how to invalidate
│   ├── Caching.md                # staleTime, gcTime
│   └── Optimistic Updates.md     # Instant UI feedback
│
└── Patterns/
    ├── Loading UI.md             # Skeletons, spinners, suspense
    ├── Error Boundaries.md       # Graceful error handling
    └── Pagination.md             # Offset vs cursor
```

### Связь с другими папками
- `Fundamentals/` опирается на `[[Web Concepts/Network/HTTP Basics]]`
- `React Integration/` использует `[[React/Hooks/useEffect]]`
- `TanStack Query/` — это **замена** для `useEffect + fetch` в большинстве случаев

---

## 🌐 Fundamentals

Базовые инструменты работы с API.

### Topics
- [[Fetch API]] — нативный способ HTTP-запросов
- [[Axios]] — популярная библиотека, interceptors
- [[HTTP Methods in Practice]] — GET, POST, PUT, PATCH, DELETE
- [[Request Headers]] — Content-Type, Authorization
- [[Error Handling]] — HTTP errors vs network errors
- [[Response Handling]] — JSON parsing, status codes

### 💡 Fetch vs Axios
```typescript
// Fetch — нужно проверять response.ok
const response = await fetch('/api/users');
if (!response.ok) throw new Error('Failed');
const data = await response.json();

// Axios — автоматический throw при ошибке
const { data } = await axios.get('/api/users');
```

### Key Questions (Interview)
- Разница между fetch и axios?
- Как обработать 404 ошибку в fetch?
- Что такое interceptors в axios?

---

## ⚛️ React Integration

Как правильно делать запросы в React.

### Topics
- [[useEffect Fetching]] — классический подход
- [[Custom Fetch Hook]] — useFetch, абстракция логики
- [[Loading States]] — loading, error, data pattern
- [[Race Conditions]] — cleanup и AbortController
- [[Optimistic Updates]] — UI без ожидания сервера

### 💡 Basic Fetch Pattern
```typescript
function useUsers() {
  const [data, setData] = useState<User[] | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);

  useEffect(() => {
    const controller = new AbortController();
    
    fetch('/api/users', { signal: controller.signal })
      .then(res => res.json())
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false));
    
    return () => controller.abort(); // Cleanup!
  }, []);

  return { data, loading, error };
}
```

### ⚠️ Common Gotchas
- Забытый cleanup → memory leaks, race conditions
- Запрос в render без useEffect
- Не обрабатывать loading/error states

---

## 🔄 TanStack Query

Современный подход к серверному состоянию.

### Topics
- [[Query Basics]] — useQuery, queryKey, queryFn
- [[Mutations]] — useMutation, onSuccess, onError
- [[Query Invalidation]] — когда и как инвалидировать
- [[Caching]] — staleTime, gcTime (cacheTime)
- [[Optimistic Updates]] — мгновенный UI feedback
- [[Infinite Queries]] — пагинация, бесконечный скролл
- [[Prefetching]] — предзагрузка данных

### 💡 Basic useQuery
```typescript
import { useQuery } from '@tanstack/react-query';

function useUsers() {
  return useQuery({
    queryKey: ['users'],
    queryFn: () => fetch('/api/users').then(res => res.json()),
    staleTime: 5 * 60 * 1000, // 5 минут "свежести"
  });
}

// В компоненте
const { data, isLoading, error } = useUsers();
```

### 💡 Mutation with Invalidation
```typescript
const mutation = useMutation({
  mutationFn: (newUser: User) => 
    fetch('/api/users', {
      method: 'POST',
      body: JSON.stringify(newUser),
    }),
  onSuccess: () => {
    queryClient.invalidateQueries({ queryKey: ['users'] });
  },
});
```

### Key Questions (Interview)
- Зачем нужен TanStack Query если есть useEffect?
- Что такое staleTime vs gcTime?
- Как работает invalidation?

---

## 🎨 Patterns

Продвинутые паттерны работы с данными.

### Topics
- [[Loading UI Patterns]] — skeletons, spinners, suspense
- [[Error Boundaries]] — graceful error handling
- [[Retry Logic]] — автоматические повторы
- [[Pagination Patterns]] — offset vs cursor
- [[Polling]] — периодическое обновление данных
- [[Dependent Queries]] — запросы, зависящие друг от друга

### 💡 Error Boundary + Suspense
```typescript
<ErrorBoundary fallback={<ErrorMessage />}>
  <Suspense fallback={<Skeleton />}>
    <UserList />
  </Suspense>
</ErrorBoundary>
```

---

## 🔐 Security Angle

> Критически важно для безопасности:
> - **Никогда** не храни токены в localStorage (XSS уязвимость)
> - Используй httpOnly cookies для auth tokens
> - Валидируй ответы сервера (Zod)
> - Sanitize данные перед отображением

### Secure Token Pattern
```typescript
// ❌ Плохо — XSS может украсть токен
localStorage.setItem('token', token);

// ✅ Лучше — httpOnly cookie (сервер устанавливает)
// Токен недоступен из JS
```

---

## 🔗 Connections

- [[_React Map]] — fetching в контексте React
- [[_TypeScript Map]] — типизация API responses
- [[_Web Concepts Map]] — HTTP, CORS fundamentals
- [[_Security Map]] — безопасная работа с данными

---

## 📈 Progress

### Must Know (Junior)
- [ ] Fetch API basics
- [ ] useEffect + fetch pattern
- [ ] Loading/Error states
- [ ] Cleanup & AbortController

### Must Know (Junior+)
- [ ] TanStack Query basics
- [ ] Mutations & invalidation
- [ ] Caching concepts
- [ ] Error boundaries

### Good to Know
- [ ] Optimistic updates
- [ ] Infinite queries
- [ ] Prefetching strategies

---

*Part of [[_Frontend Development Map]]*
