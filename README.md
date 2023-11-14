## Как мокать данные с сервера

_Шаг 1_: **создаем db.json**

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
  
_Шаг 2_: **Устанавливаем json-server**  
  
```
npm install -g json-server
```
  
_Шаг 3_: **Стартуем JSON-сервер**  
  
```
json-server --watch db.json --port 3030
```  
Note: React utilizes the 3000 port, which json-server uses to run the server, thus we used — port 3030 to modify the port.
  
_Шаг 4:_ **Тестируем API**  
  
Тепер, если открыть http://localhost:3030/posts мы сможем увидеть data
![image](https://github.com/Highflyingexpress/frontend-tricks/assets/107925514/c6fc10a5-843e-4c2a-ab2b-b1cdc8a6b6a9)
_Шаг 5:_ **Делаем API запрос в React**   
например классический пример:  
```React
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

## Архитектура. Как не писать в импортах длинные пути к файлам.
  
**public-api.ts + index.ts**   
1) `index.ts` в каждой папке, который экспортирует все файлы из папки  
2) затем в `public-api.ts` собираем все экспорты из всех папок

Пример структуры проекта:
```
/src
  /moduleA
    - fileA1.ts
    - fileA2.ts
    - index.ts
  /moduleB
    - fileB1.ts
    - fileB2.ts
    - index.ts
  /moduleC
    - fileC1.ts
    - fileC2.ts
    - index.ts
  - public-api.ts
```
Пример содержимого файлов index.ts:
```
// moduleA/index.ts
export * from './fileA1';
export * from './fileA2';

// moduleB/index.ts
export * from './fileB1';
export * from './fileB2';

// moduleC/index.ts
export * from './fileC1';
export * from './fileC2';

// public-api.ts
export * from './moduleA';
export * from './moduleB';
export * from './moduleC';
```

`public-api.ts` собирает все экспорты в одном месте   
```
  // Другие файлы в проекте
import { someFunctionFromModuleA, someVariableFromModuleB } from './public-api';  
```

## Basic fetching data with useTransition  
today weather in Saint.P  
```typescript
import React, { useEffect, useState, useTransition } from "react";

interface Location {  country: string; }
interface Current {  temp_c: number; }
interface WeatherResponse {
  location: Location;
  current: Current;
}

const api = "b187fa2d8b7047e88f780241231411"; // api key

const App: React.FC = () => {
  const [data, setData] = useState<WeatherResponse | null>(null);
  const [isPending, startTransition] = useTransition(); // React 18' hook was born

  useEffect(() => {
    const fetchData = async (): Promise<void> => {
      try {
        await startTransition(async () => {
          const response = await fetch(
            `https://api.weatherapi.com/v1/current.json?key=${api}&q=Saint-Petersburg&aqi=no`
          );

          if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
          }

          const responseData: WeatherResponse = await response.json();
          setData(responseData);
        });
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    };

    fetchData();
  }, []); // empty dependency array for initial render

  return (
    <div>
      {isPending ? (
        <p>Loading...</p>
      ) : (
        data && (
          <>
            <h1>{data.location.country}</h1>
            <p>Temperature: {data.current.temp_c}°C</p>
          </>
        )
      )}
    </div>
  );
};

export default App;
```




