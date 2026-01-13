# Coercion

> Implicit vs Explicit type conversion — источник "странностей" JavaScript.

---

## Explicit Coercion (Явное преобразование)

### К строке
<!-- String(), .toString(), template literals -->

### К числу
<!-- Number(), parseInt(), parseFloat(), унарный + -->

### К boolean
<!-- Boolean(), двойное отрицание !! -->

---

## Implicit Coercion (Неявное преобразование)

### Когда JS преобразует автоматически?
<!-- операторы, сравнения, логический контекст -->

### Оператор + со строками
<!-- "5" + 3, 3 + "5", [] + {} -->

### Оператор - и другие математические
<!-- "5" - 3, "5" * "2" -->

---

## == vs === 

### Алгоритм == (Abstract Equality)
<!-- шаги сравнения с приведением типов -->

### Почему === безопаснее?
<!-- no coercion, predictable -->

### Таблица сравнений
<!-- заполни результаты -->

| Expression           | Result | Why? |
| -------------------- | ------ | ---- |
| `1 == "1"`           | true   |      |
| `1 === "1"`          | false  |      |
| `null == undefined`  |        |      |
| `null === undefined` |        |      |
| `0 == false`         | true   |      |
| `0 == ""`            | true   |      |
| `[] == false`        |        |      |
| `[] == ![]`          |        |      |

---

## Object to Primitive

### ToPrimitive алгоритм
<!-- valueOf(), toString(), Symbol.toPrimitive -->

### Почему `[] + [] === ""`?
<!-- пошаговое объяснение -->

### Почему `[] + {} === "[object Object]"`?
<!-- пошаговое объяснение -->

### Почему `{} + [] === 0`? (в консоли)
<!-- block vs object literal -->

---

## Truthy и Falsy

### Полный список falsy values
<!-- 6 значений -->

### Всё остальное — truthy
<!-- включая "0", [], {} -->

### Проверка в условиях
<!-- if (value) — что это значит? -->

---

## Gotchas

### `NaN === NaN` → false
<!-- почему и как проверять NaN -->

### `typeof NaN === "number"`
<!-- да, NaN это number -->

### Сравнение объектов
<!-- {} === {} → false, всегда по reference -->

---

## Best Practices

### Когда использовать `==?`
<!-- почти никогда, исключение: null == undefined -->

### ESLint правило eqeqeq
<!-- как настроить -->

---

## Interview Questions

- Чем отличается `==` от `===`?
- Что вернёт `[] + {}`? Почему?
- Какие значения falsy в JavaScript?
- Как безопасно проверить на NaN?
- Объясни `[] == ![]`
