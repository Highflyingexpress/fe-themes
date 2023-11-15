[resource](https://gist.github.com/zmts/802dc9c3510d79fd40f9dc38a12bccfc)  
[medium](https://medium.com/nuances-of-programming/%D0%BF%D0%BE%D0%BB%D0%BD%D0%BE%D0%B5-%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-%D0%BF%D0%BE-%D1%83%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D1%8E-jwt-%D0%B2%D0%BE-%D1%84%D1%80%D0%BE%D0%BD%D1%82%D0%B5%D0%BD%D0%B4-%D0%BA%D0%BB%D0%B8%D0%B5%D0%BD%D1%82%D0%B0%D1%85-graphql-b9b5103062a3)  
[статья](https://habr.com/ru/articles/710552/)

![image](https://github.com/Highflyingexpress/frontend-tricks/assets/107925514/46e99a71-e504-4c0b-911a-7b5780c9c71f)  

**CSRF**  Cross-Site Request Forgery (CSRF) - атака, при которой происходит выполнение несанкционированного запроса от лица пользователя к ресурсу, на котором пользователь в данный момент аутентифицирован  
**XSS** Cross-Site Scripting (XSS) - атака, подразумевающая внедрение злоумышленником и исполнение в браузере жертвы [вредоносного] JavaScript-кода.   

  ![image](https://github.com/Highflyingexpress/frontend-tricks/assets/107925514/02adb7b3-5005-4dce-8bfc-69b379acc6ca)
  
## js-cookie  lib

`npm install js-cookie`

```javascript
import React, { useState, useEffect } from 'react';
import Cookies from 'js-cookie';

const App = () => {
  // Assume you have some functions to handle authentication and obtain tokens
  const [accessToken, setAccessToken] = useState(Cookies.get('access_token') || '');
  const [refreshToken, setRefreshToken] = useState(Cookies.get('refresh_token') || '');

  // Example function to handle authentication and set tokens
  const handleAuthentication = async () => {
    // Make a request to your authentication endpoint
    // Assuming it returns tokens in the response
    const response = await authenticateUser();

    // Update state and set cookies with httpOnly flag
    setAccessToken(response.accessToken);
    setRefreshToken(response.refreshToken);
    Cookies.set('access_token', response.accessToken, { path: '/', httpOnly: true });
    Cookies.set('refresh_token', response.refreshToken, { path: '/', httpOnly: true });
  };

  // Example function to refresh the access token using the refresh token
  const refreshAccessToken = async () => {
    // Make a request to your token refresh endpoint with the refresh token
    // Assuming it returns a new access token in the response
    const response = await refreshTokens(refreshToken);

    // Update state and set the new access token cookie with httpOnly flag
    setAccessToken(response.accessToken);
    Cookies.set('access_token', response.accessToken, { path: '/', httpOnly: true });
  };

  // Example useEffect to refresh the access token when it's expired
  useEffect(() => {
    const checkAccessToken = async () => {
      // Check if the access token is expired
      if (isAccessTokenExpired(accessToken)) {
        // If expired, refresh the access token
        await refreshAccessToken();
      }
    };

    checkAccessToken();
  }, [accessToken, refreshAccessToken]);

  return (
    <div>
      {/* Your application content */}
    </div>
  );
};

export default App;
```
  

## токены в Redux  

```
// экшн для сохранения токенов в состоянии Redux

const setTokens = (accessToken, refreshToken) => ({
  type: 'SET_TOKENS',
  payload: { accessToken, refreshToken },
});

// редьюсер для обновления состояния с токенами

const authReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'SET_TOKENS':
      return {
        ...state,
        accessToken: action.payload.accessToken,
        refreshToken: action.payload.refreshToken,
      };
    // Другие кейсы и логика
    default:
      return state;
  }
};

// Пример использования в компоненте React
// Вызывается при успешной аутентификации
dispatch(setTokens(accessToken, refreshToken));

// При истечении срока действия токена доступа
// Используем рефреш-токен для получения нового токена доступа

const newAccessToken = await fetchNewAccessToken(refreshToken);
dispatch(setTokens(newAccessToken, refreshToken));
```


