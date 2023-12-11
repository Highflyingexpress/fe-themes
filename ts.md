```javascript
import { Button } from "./button";
import { bindProps } from "./bind-props";
const RedButton = bindProps(Button,
  {
    className: "mt-4 bg-red-500",
    type: "button",
    style: {
      marginTop:
    }
  });

export default function App() {
  return (
    <div className="App">
      <RedButton>Новости</RedButton>
    </div>
  ) ;
}

```

### JSX global

```typescript
// global.d.ts

declare namespace JSX {
  interface IntrinsicElements {
    [elementName: string]: any;
  }
}
```

---
  
```typescript
type CheckString<T> = T extends string ? true : false;

const isString: CheckString<number> = false;
const isString2: CheckString<string> = true;
```

as используется для явного приведения типов:  
```typescript
const someValue: any = "Hello, TypeScript!";
const strLength: number = (someValue as string).length;
```

