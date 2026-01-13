# Day 3: Async/Await - What I Learned

## Core Concepts

- `async` keyword makes function return Promise
- `await` pauses execution until Promise resolves, only works inside `async` functions
- `try/catch` for error handling in async functions

## Aha Moments

- Асинхронные функции работают в Event Loop также как и вызов new Promise

## Struggled With

- Тема легкая, нужно просто больше практики. Также добавлю что не считаю синтаксис async/await лучше, но все равно буду писать теперь только так

## Sequential vs Parallel - THE KEY RULE

### When Sequential (operations depend on each other)

```javascript
const post = await getPost(id);
const user = await getUser(post.userId); // Needs post data!
```

### When Parallel (operations are independent)

```javascript
const [users, posts] = await Promise.all([getUsers(), getPosts()]); // Both fetch at same time!
```

## Performance Impact

- Sequential 3 fetches: ~1500ms
- Parallel 3 fetches: ~500ms
- **3x faster with Promise.all()!**

## Code I'm Proud Of

```javascript
async function loadUserProfile(userId) {
  const user = await fetch(`/api/users/${userId}`).then((r) => r.json());

  const [posts, friends] = await Promise.all([
    fetch(`/api/posts?userId=${userId}`).then((r) => r.json()),
    fetch(`/api/friends?userId=${userId}`).then((r) => r.json()),
  ]);

  const firstPostComments = await fetch(
    `/api/comments?postId=${posts[0].id}`
  ).then((r) => r.json());
  return { user, posts, friends, firstPostComments };
}
```

## Common Patterns

### Pattern 1: Basic async/await

```javascript
async function getData() {
  const response = await fetch(url);
  const data = await response.json();
  return data;
}
```

### Pattern 2: Error handling

```javascript
async function getData() {
  try {
    const response = await fetch(url);
    if (!response.ok) throw new Error("HTTP error");
    return await response.json();
  } catch (error) {
    console.error(error);
    throw error;
  }
}
```

### Pattern 3: Parallel execution

```javascript
const [data1, data2, data3] = await Promise.all([
  fetch(url1).then((r) => r.json()),
  fetch(url2).then((r) => r.json()),
  fetch(url3).then((r) => r.json()),
]);
```

### Pattern 4: Mixed (sequential + parallel)

```javascript
const user = await getUser(); // Sequential (need user first)

const [posts, friends] = await Promise.all([
  // Parallel (independent)
  getPosts(user.id),
  getFriends(user.id),
]);
```

## Questions for Tomorrow

- Узнать больше о паттернах обработки ошибок

## English Terms Learned

- await - ждать/приостановить
- async - асинхронный
- parallel execution - параллельное выполнение
- sequential execution - последовательное выполнение
- resolve - разрешить (Promise)

## Key Takeaway

**If operations are independent → use Promise.all() for parallel execution!** - This single rule can make your code 2-5x faster.