## Как мокать данные с сервера

_Шаг 1_: создаем db.json

```json

{
    "posts": [
      {
        "id": 1,
        "title": "Create a login form using formik in react js",
        "body": "Todays article will demonstrate how to develop a login form in react js using formik."
      },
      {
        "id": 2,
        "title": "How to parse or read CSV files in ReactJS",
        "body": "In this article, I will teach you how to parse or read CSV files in ReactJS in the simplest way possible. "
      }
    ]
  }
```

_Шаг 2_: Устанавливаем json-server  
```
npm install -g json-server
```
  
_Шаг 3_: Стартуем JSON-сервер  
```
json-server --watch db.json --port 3030
```  
Note: React utilizes the 3000 port, which json-server uses to run the server, thus we used — port 3030 to modify the port.
  
_Шаг 4:_ Тестируем API  
Тепер, если открыть http://localhost:3030/posts мы сможем увидеть data
![image](https://github.com/Highflyingexpress/frontend-tricks/assets/107925514/c6fc10a5-843e-4c2a-ab2b-b1cdc8a6b6a9)

_Шаг 5:_ Делаем API запрос в React  
например классический пример:  
```
import React, { useState, useEffect } from "react";

const App = () => {
  const [posts, setPosts] = useState([]);

  const getData = () => {
    var requestOptions = {
      method: "GET",
      redirect: "follow",
    };

    fetch("http://localhost:3030/posts", requestOptions)
      .then((response) => response.json())
      .then((result) => setPosts(result))
      .catch((error) => console.log("error", error));
  };

  useEffect(() => {
    getData();
  }, []);

  return (
    <div>
      {posts.map((post) => (
        <div key={post.id}>
          <h3>
            <span>{post.id}</span> {post.title}
          </h3>
          <p>{post.body}</p>
        </div>
      ))}
    </div>
  );
};

export default App;
```

Доступны все операции  
**POST**  
![image](https://github.com/Highflyingexpress/frontend-tricks/assets/107925514/490cbe5b-92c5-498b-bb51-29dbb078d6ed)

**PUT**  
![image](https://github.com/Highflyingexpress/frontend-tricks/assets/107925514/c5b8d2b0-24e5-4792-b37d-aee1435f9240)

**DELETE**  
![image](https://github.com/Highflyingexpress/frontend-tricks/assets/107925514/ab0a1cbb-0ea1-41eb-8c01-3ee93efa2257)



