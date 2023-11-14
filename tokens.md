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

    // Update state and set cookies
    setAccessToken(response.accessToken);
    setRefreshToken(response.refreshToken);
    Cookies.set('access_token', response.accessToken, { path: '/' });
    Cookies.set('refresh_token', response.refreshToken, { path: '/' });
  };

  // Example function to refresh the access token using the refresh token
  const refreshAccessToken = async () => {
    // Make a request to your token refresh endpoint with the refresh token
    // Assuming it returns a new access token in the response
    const response = await refreshTokens(refreshToken);

    // Update state and set the new access token cookie
    setAccessToken(response.accessToken);
    Cookies.set('access_token', response.accessToken, { path: '/' });
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


