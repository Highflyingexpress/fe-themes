
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


