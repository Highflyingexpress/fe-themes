#### Types vs Interface  

https://www.youtube.com/watch?v=Idf0zh9f3qQ  

Type  
<img src="https://github.com/Highflyingexpress/fe-themes/assets/107925514/f7487b55-614c-4a01-93e9-059c7a6c7fb0" width=400>  
Interface  
<img src="https://github.com/Highflyingexpress/fe-themes/assets/107925514/95dab563-7517-4e05-9cfe-49412102b1d8" width=500>
  
кортеж  и тип и интерфейс на скрине:  
<img src="https://github.com/Highflyingexpress/fe-themes/assets/107925514/021939c9-493d-446e-8eca-c8c9a19008a0" width=500>

##### забиндить пропсы компонента  
  
```javascript

import { ReactElement } from "react";
export function bindProps<Props extends {}, BoundKeys extends keyof Props>(
  Component: (props: Props) => ReactElement,
  boundProps: Pick<Props, BoundKeys>,
  displayName?: string
  function ResultCompoent(newProps: Omit<Props, BoundKeys>) {
    const props = { …boundProps, …newProps } as Props;
    return <Component {…props} />;
I }
  ResultCompoent.displayName displayName ?? Component.name + "WithProps";

  return ResultCompoent;
}

```

  применение:
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
видео https://youtu.be/18D0wpbCw8E?si=4h9cxiGoF7C0qXDj


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

