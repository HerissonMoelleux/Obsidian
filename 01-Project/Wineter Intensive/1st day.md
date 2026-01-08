# Day 1: Promises - What I Learned
## Core Concepts

- Promise has 3 states: pending, fulfilled, rejected
- `new Promise((resolve, reject) => {})` creates a promise
- `.then()` handles success, `.catch()` handles errors
- Each `.then()` returns a new Promise
## Aha Moments

- Executor function - runs immediately, this means that the synchronous function called inside will also be executed synchronously
## Struggled With

- Я слегка ошибался в работе Event Loop. Задачи не переходят из Macrotask Queue -> Microtask Queue -> Callback Stack. Они сразу же создаются внутри этих очердей.
## Code I'm Proud Of

```javascript
function riskyOperation(state) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (state) {
        resolve("Operation succeeded");
      } else {
        reject("Operation failed");
      }
    }, 10);
  });
}

riskyOperation(true)
  .then((message) => {
    console.log(`Step 1: ${message}`);
    return riskyOperation(true);
  })
  .then((message) => {
    console.log(`Step 2: ${message}`);
    return riskyOperation(false);
  })
  .catch((message) => {
    console.log(`Step 3: ${message}`);
    return "Recovered from error";
    // return riskyOperation(...) <- Or we may continue the chain
  });

```

  

## Questions for Tomorrow

- Need to repeat `Callback`
- В целом тема `Promise` легкая в понимании, только нужно больше практики
## English Terms Learned

- Promise - обещание
- resolve - разрешить/выполнить
- reject - отклонить
- pending - в ожидании
- fulfilled - выполнено
- executor - исполнитель