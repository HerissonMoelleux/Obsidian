# Day 2: Fetch API - What I Learned

## Core Concepts

- fetch() returns a Promise
- response.json() also returns a Promise
- HTTP methods: GET, POST, PUT, DELETE
- response.ok checks if status is 200-299

## Aha Moments

- Я столкнулся с ошибкой в коде и узнал о том что браузер всегда требует от нас помечать ассинхроность. И если мы пользуемся await то при вызове должны либо дать тип нашему скрипту `<script type="module" src="./2nd day/fetch.js"></script>` либо использовать конструкцию `(async () => {})();`
- Удивительно что в url можно с конструкциями: `https://jsonplaceholder.typicode.com/posts?userId=${userId}` находить посты по id пользователя

## Struggled With

- Иногда путался в цепочках Promises
- Плохо понял как работать с POST/DELETE/PUT/PATCH, а именно плохо замонил что должно лежать в options -> fetch(url, options={...})

## Code I'm Proud Of

```javascript
function searchPost(userId) {
  return fetch(
    `https://jsonplaceholder.typicode.com/posts?userId=${userId}`
  ).then((response) => {
    return response.json();
  });
}

fetch("https://jsonplaceholder.typicode.com/users")
  .then((response) => response.json())
  .then((users) => {
    const promises = users.map((user) => {
      return searchPost(user.id).then((posts) => {
        return { name: user.name, length: posts.length, posts: posts };
      });
    });

    return Promise.all(promises);
  })
  .then((results) => {
    console.log(results);
    console.log(`Number of users - ${results.length}`);
    results.forEach((response) => console.log(`${response.name}`));
    let postsCount = 0;
    results.forEach((response) => {
      postsCount += response.length;
      console.log(
        `Posts by ${response.name}, number of posts - ${response.length}`
      );
      response.posts.forEach((post) => console.log(post.title));
    });
    const userMostPosts = results.reduce((prev, current) => {
      return prev.length > current.length ? prev : current;
    });
    console.log("User with most posts:", userMostPosts);
    console.log(`Total number of posts from all users - ${postsCount}!`);
  })
  .catch((error) => console.error("Ошибка:", error));
```

## Common Mistakes I Made

- Forgetting to return response.json()
- Not checking response.ok

## Questions for Tomorrow

- Что такое CORS?
- Как устроен скелет запроса?

## English Terms Learned

- fetch - получить/извлечь
- response - ответ
- endpoint - конечная точка API
- payload - данные запроса