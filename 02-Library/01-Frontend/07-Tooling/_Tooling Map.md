# Tooling Map

> Инструменты, которые делают разработку эффективной.

---

## 🎯 Почему эта папка существует?

Инструменты — **часть профессии**. Нельзя быть разработчиком и не знать Git, npm, линтеры.

**Аналогия:** Мастерская со станками. Можно быть талантливым столяром, но без инструментов мебель не сделаешь.

---

## 📁 Structure

```
07-Tooling/
├── Package Managers/
│   ├── npm Basics.md             # install, scripts, audit
│   ├── package.json.md           # Structure, dependencies
│   └── pnpm.md                   # Fast alternative
│
├── Build Tools/
│   ├── Vite.md                   # ⭐ Why Vite, how it works
│   ├── Vite Config.md            # Plugins, aliases, env
│   └── Environment Variables.md  # .env files, security
│
├── Code Quality/
│   ├── ESLint.md                 # Linting setup
│   ├── Prettier.md               # Formatting
│   ├── ESLint + Prettier.md      # Integration
│   └── Husky.md                  # Pre-commit hooks
│
└── Version Control/
    ├── Git Fundamentals.md       # add, commit, push, pull
    ├── Branching.md              # Feature branches, strategies
    ├── Conventional Commits.md   # ⭐ Structured messages
    └── .gitignore.md             # What to exclude
```

---

## 📦 Package Managers

Управление зависимостями проекта.

### Topics
- [[npm Basics]] — install, update, scripts
- [[package.json]] — dependencies, devDependencies, scripts
- [[package-lock.json]] — зачем нужен, когда коммитить
- [[pnpm]] — быстрая альтернатива npm
- [[Semantic Versioning]] — ^, ~, exact versions
- [[npx]] — выполнение пакетов без установки

### 💡 package.json Scripts
```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "test": "vitest",
    "lint": "eslint . --ext .ts,.tsx",
    "format": "prettier --write ."
  }
}
```

### Key Questions (Interview)
- Разница между dependencies и devDependencies?
- Что значит `^1.2.3` vs `~1.2.3`?
- Зачем коммитить lock-файл?

---

## 🔧 Build Tools

Сборка и development server.

### Topics
- [[Vite Basics]] — почему Vite, как работает
- [[Vite Config]] — plugins, aliases, env variables
- [[Environment Variables]] — .env files, import.meta.env
- [[Build Output]] — chunks, assets, optimization
- [[Dev Server]] — HMR, proxy

### 💡 Vite Config Example
```typescript
// vite.config.ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'path';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
  server: {
    proxy: {
      '/api': 'http://localhost:3000',
    },
  },
});
```

### 💡 Environment Variables
```bash
# .env
VITE_API_URL=https://api.example.com

# .env.development
VITE_API_URL=http://localhost:3000
```

```typescript
// Usage
const apiUrl = import.meta.env.VITE_API_URL;
```

### 🔐 Security Note
> **НИКОГДА** не храни секреты в .env для фронтенда!
> Все VITE_* переменные видны в браузере.
> API keys, secrets → только на бэкенде.

---

## ✨ Code Quality

Автоматическое поддержание качества кода.

### Topics
- [[ESLint Setup]] — конфигурация, правила
- [[Prettier Setup]] — форматирование кода
- [[ESLint + Prettier]] — интеграция без конфликтов
- [[Husky]] — git hooks
- [[lint-staged]] — линтинг только staged файлов
- [[EditorConfig]] — консистентность между редакторами

### 💡 Recommended ESLint Config
```javascript
// eslint.config.js (flat config)
import js from '@eslint/js';
import typescript from '@typescript-eslint/eslint-plugin';
import react from 'eslint-plugin-react';
import reactHooks from 'eslint-plugin-react-hooks';

export default [
  js.configs.recommended,
  {
    plugins: {
      '@typescript-eslint': typescript,
      react,
      'react-hooks': reactHooks,
    },
    rules: {
      'react-hooks/rules-of-hooks': 'error',
      'react-hooks/exhaustive-deps': 'warn',
    },
  },
];
```

### 💡 Pre-commit Hook Setup
```bash
# Install
npm install -D husky lint-staged

# Setup
npx husky init
echo "npx lint-staged" > .husky/pre-commit
```

```json
// package.json
{
  "lint-staged": {
    "*.{ts,tsx}": ["eslint --fix", "prettier --write"],
    "*.{json,md}": ["prettier --write"]
  }
}
```

---

## 📚 Version Control

Git — must have для любого разработчика.

### Topics
- [[Git Fundamentals]] — add, commit, push, pull
- [[Branching Strategies]] — feature branches, GitFlow lite
- [[Conventional Commits]] — структурированные commit messages
- [[Pull Requests]] — review process, description
- [[.gitignore]] — что не коммитить
- [[Git Stash]] — временное сохранение изменений

### 💡 Conventional Commits
```bash
# Format: type(scope): description

feat(auth): add login form validation
fix(api): handle network timeout errors
docs(readme): update installation steps
refactor(hooks): extract useFetch logic
test(button): add click handler tests
chore(deps): update dependencies
```

### 💡 Good .gitignore
```gitignore
# Dependencies
node_modules/

# Build
dist/
build/

# Environment
.env
.env.local
.env.*.local

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Logs
*.log
npm-debug.log*
```

### Key Questions (Interview)
- Как решить merge conflict?
- Разница между merge и rebase?
- Зачем нужны conventional commits?

---

## 🔗 Connections

- [[_React Map]] — Vite для React проектов
- [[_TypeScript Map]] — ESLint + TypeScript
- [[_Testing Map]] — test scripts в package.json

---

## 📈 Progress

### Must Know (Junior)
- [ ] npm basics (install, scripts)
- [ ] package.json structure
- [ ] Vite dev server & build
- [ ] Git fundamentals
- [ ] Basic .gitignore

### Must Know (Junior+)
- [ ] ESLint + Prettier setup
- [ ] Husky pre-commit hooks
- [ ] Environment variables
- [ ] Conventional commits
- [ ] Branching strategies

### Good to Know
- [ ] pnpm, yarn
- [ ] Vite plugins
- [ ] GitHub Actions basics

---

*Part of [[_Frontend Development Map]]*
