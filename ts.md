## JSX global

``typescript
// global.d.ts

declare namespace JSX {
  interface IntrinsicElements {
    [elementName: string]: any;
  }
}
```
