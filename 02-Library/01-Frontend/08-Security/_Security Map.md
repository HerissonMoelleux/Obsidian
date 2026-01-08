# Security Map

> Твоя суперсила. Cybersecurity background даёт преимущество над другими джунами.

---

## 🎯 Почему эта папка существует?

**Твоё конкурентное преимущество.** Большинство джунов не думают о безопасности. Ты — думаешь, потому что Cybersecurity background.

**Аналогия:** Замки на дверях. Можно построить красивый дом, но без защиты его ограбят.

---

## 📁 Structure

```
08-Security/
├── Frontend Vulnerabilities/
│   ├── XSS.md                    # ⭐ Types, React protection
│   ├── CSRF.md                   # Attack mechanism, protection
│   ├── Clickjacking.md           # UI redressing
│   └── Open Redirects.md         # Redirect vulnerabilities
│
├── Secure Coding/
│   ├── Input Validation.md       # Client + server validation
│   ├── Zod as Security.md        # Runtime validation
│   ├── Sanitization.md           # DOMPurify for HTML
│   └── CSP.md                    # Content Security Policy
│
└── Authentication/
    ├── JWT Basics.md             # Structure, claims
    ├── Token Storage.md          # ⭐ Where NOT to store
    ├── httpOnly Cookies.md       # Secure pattern
    └── OAuth Basics.md           # Frontend flow
```

---

## 🔓 Frontend Vulnerabilities

Уязвимости, специфичные для фронтенда.

### Topics
- [[XSS (Cross-Site Scripting)]] — типы, примеры, защита
- [[CSRF (Cross-Site Request Forgery)]] — механизм атаки
- [[Injection Attacks]] — SQL, NoSQL, command injection (frontend role)
- [[Clickjacking]] — UI redressing attacks
- [[Open Redirects]] — опасность непроверенных редиректов
- [[Sensitive Data Exposure]] — утечки через клиент

### 💡 XSS Types
```
Stored XSS    — вредоносный код сохранён на сервере
Reflected XSS — код в URL, отражается в ответе
DOM-based XSS — манипуляция DOM без участия сервера
```

### 💡 React's XSS Protection
```typescript
// ✅ React автоматически экранирует
const userInput = '<script>alert("xss")</script>';
return <div>{userInput}</div>; // Безопасно — отрендерится как текст

// ❌ ОПАСНО — dangerouslySetInnerHTML
return <div dangerouslySetInnerHTML={{ __html: userInput }} />;
// Используй ТОЛЬКО для санитизированного HTML
```

### Key Questions (Interview)
- Как React защищает от XSS?
- Когда XSS всё ещё возможен в React?
- Что такое CSRF и как защититься?

---

## 🛡️ Secure Coding

Практики безопасного кода.

### Topics
- [[Input Validation]] — валидация на клиенте и сервере
- [[Output Encoding]] — правильное экранирование
- [[Sanitization]] — DOMPurify для HTML
- [[Content Security Policy]] — CSP headers
- [[Secure Dependencies]] — npm audit, Snyk
- [[Error Handling Security]] — не раскрывай stack traces

### 💡 Zod as Security Layer
```typescript
import { z } from 'zod';

// Не просто типы — это валидация!
const UserInputSchema = z.object({
  email: z.string().email().max(255),
  name: z.string().min(1).max(100).regex(/^[a-zA-Z\s]+$/),
  age: z.number().int().min(0).max(150),
});

// Runtime защита от malicious input
function handleSubmit(data: unknown) {
  const result = UserInputSchema.safeParse(data);
  if (!result.success) {
    // Не доверяем данным
    return;
  }
  // result.data теперь типизирован И валидирован
}
```

### 💡 Content Security Policy
```html
<!-- Защита от inline scripts -->
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline';">
```

### npm Security
```bash
# Проверить уязвимости
npm audit

# Автоматически исправить
npm audit fix

# Посмотреть детали
npm audit --json
```

---

## 🔐 Authentication

Безопасная аутентификация на фронтенде.

### Topics
- [[JWT Basics]] — structure, claims, validation
- [[Token Storage]] — где хранить токены (и где НЕ хранить)
- [[OAuth 2.0 Basics]] — flow для фронтенда
- [[Session vs Token]] — разница подходов
- [[Secure Cookie Attributes]] — HttpOnly, Secure, SameSite
- [[Refresh Token Pattern]] — безопасное обновление токенов

### 💡 Token Storage Decision
```
❌ localStorage     — XSS может украсть
❌ sessionStorage   — XSS может украсть
⚠️ Memory (JS var)  — безопасно, но теряется при refresh
✅ httpOnly Cookie  — недоступно из JS, защита от XSS
```

### 💡 Secure Auth Pattern
```typescript
// Tokens в httpOnly cookies (сервер устанавливает)
// Фронтенд не видит токен, только делает запросы

async function login(credentials: Credentials) {
  const response = await fetch('/api/auth/login', {
    method: 'POST',
    credentials: 'include', // Включает cookies!
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(credentials),
  });
  // Сервер устанавливает httpOnly cookie
  // Фронтенд не трогает токен напрямую
}

async function fetchProtectedData() {
  const response = await fetch('/api/data', {
    credentials: 'include', // Cookie отправляется автоматически
  });
  return response.json();
}
```

### Key Questions (Interview)
- Почему localStorage плохо для JWT?
- Как работает httpOnly cookie?
- Что такое refresh token и зачем он нужен?

---

## 📋 OWASP Top 10 (Frontend Relevance)

| # | Vulnerability | Frontend Role |
|---|---------------|---------------|
| 1 | Broken Access Control | UI не скрывает = не защита |
| 2 | Cryptographic Failures | Не храни sensitive data на клиенте |
| 3 | Injection | Валидация input, санитизация output |
| 4 | Insecure Design | Security с самого начала |
| 5 | Security Misconfiguration | CSP, secure headers |
| 6 | Vulnerable Components | npm audit, обновления |
| 7 | Auth Failures | Secure token storage |
| 8 | Data Integrity Failures | Validate server responses |
| 9 | Logging Failures | Не логируй sensitive data |
| 10 | SSRF | Frontend редко, но redirects опасны |

---

## 🔗 Connections

- [[_React Map]] — XSS protection в React
- [[_Data Fetching Map]] — secure API calls
- [[_Web Concepts Map]] — CORS, cookies, HTTPS
- [[_TypeScript Map]] — Zod validation

---

## 📈 Progress

### Must Know (Junior)
- [ ] XSS basics & React protection
- [ ] Why not localStorage for tokens
- [ ] Input validation importance
- [ ] npm audit

### Must Know (Junior+)
- [ ] CSRF protection
- [ ] httpOnly cookies pattern
- [ ] Zod for runtime validation
- [ ] CSP basics
- [ ] OAuth flow understanding

### Good to Know
- [ ] Full OWASP Top 10
- [ ] Penetration testing basics
- [ ] Security headers deep dive

---

## 🎯 How to Leverage This

**На собеседовании:**
> "У меня background в кибербезопасности, поэтому я автоматически думаю о XSS при работе с user input и использую Zod не только для типизации, но и как security layer..."

**В коде:**
- Комментируй security decisions
- Предлагай security improvements на code review
- Упоминай OWASP при обсуждении архитектуры

---

*Part of [[_Frontend Development Map]]*
