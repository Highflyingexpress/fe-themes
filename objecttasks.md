## Задачки с объектами
  
---
  
#### что выведет в консоль
  
```javascript

  let x = {a: 1, b: 2};

  function fn1(x) {
   x.a = 5;
  }
  function fn2() {
    x.a = 5;
  }
  function fn3(x) {
   x = 5;
  }
  function fn4() {
   x = 5;
  }
  
  fn1(x);
  console.log(x);
  
  fn2(); 
  console.log(x);
  
  fn3(x);
  console.log(x);
  
  fn4(); 
  console.log(x);
```

```javascript
let a = (};
const fn = (a) => {
   a.prop = 'hello';
   a = null;
}
fn(a);
console.log(a);
  
// все аргументы функции являются локальными переменными
// но имея общую ссылку мы можем менять объект
  
```
  
---

#### опять что в консоль  

```javascript

const fn = () => console.log(this.prop);

const o = {
  prop: 'prop',
  method() {
    fn();
  }
}

o.method();

//////////////

const o = {
  prop: 'prop',
  method() {
    const fn = () => console.log(this.prop);
    fn();
  }
}

o.method();

```


#### Написать функцию, которая суммирует все значения дерева. решить без рекурсии. Вложенность объекта любая  
```javascript
const Tree = {
  val: 12,
  left: {
    val: 24,
    left: {
      val: 24,
    },
    right: {
      val: 15,
    },
  },
  right: {
    val: 13,
    left: {
      val: 23,
    },
  },
};

const funcFunc = (obj) => {};

console.log(funcFunc(Tree)); // 111
// 12 + 24 + 24 + 15 + 13 + 23 = 111
```  
<details><summary> </summary>

```javascript
  const funcFunc = (obj) => {
    let result = 0
    let stack = [obj]
                 
    while (stack.length) {
      let node = stack.pop()
      
      for (let key in node) {
        if (typeof node[key] === 'object' && node[key]!== null) {
           stack.push(node[key])      
        }
          if ( typeof node[key] === 'number') result+=node[key]
      }
    }
    return result
  };
  
  console.log(funcFunc(Tree)); // 111
  // 12 + 24 + 24 + 15 + 13 + 23 = 111
```
</details>
  
---
  
#### Из Массива Объектов сделать Объект, ключами которого будут все встречающиеся gender, а значениями массив объектов юзеров
```javascript
const users1 = [
  {
    id: 1,
    name: "Виктория",
    gender: "female",
  },
  {
    id: 2,
    name: "Андрей",
    gender: "male",
  },
  {
    id: 3,
    name: "Александр",
    gender: "male",
  },
];

const funcObj = (arr) => {};

console.log(funcObj(users1)); //{ female: [ { id: 1, name: 'Виктория' } ],
                              // male: [ { id: 2, name: 'Андрей' }, { id: 3, name: 'Александр' } ] }
```  
<details><summary> </summary>

```javascript
  const funcObj = (arr) => {
  let returnObj = {}
  for (let obj of arr) {
    // на всякий случай проверяем есть ли вообще ключ gender
    if (obj['gender']) { 
      let {gender, ...rest} = obj // вытягиваем gender и всё остальное
      if (returnObj[gender]) returnObj[gender].push(rest) // если уже в объекте заходил гендер - пушим всё остальное
      else returnObj[gender] = [rest] // если не было такого гендера, то присваиваем ибо впервые
    }
  }
  return returnObj
};
```
</details>
  
---
  
#### плющим объект

```javascript
const arr1 = [
  {
    id: 1,
    next: [{ id: 2 }, { id: 3 }, { id: 4 }],
  },
  { id: 5, next: [{ id: 6 }, { id: 7 }, { id: 8 }] },
];


function flattenObj(arr) {}

console.log(flattenObj(arr1));
  //[ { id: 1 },
  // { id: 2 },
  // { id: 3 },
  // { id: 4 },
  // { id: 5 },
  // { id: 6 },
  // { id: 7 },
  // { id: 8 } ]
```
<details><summary> </summary>

```javascript
 function flattenObj(arr) {
   let res = []
   let stack = [...arr]

    while (stack.length) {
      let node = stack.pop()
      for (let key in node) {
        if (key === 'id') res.push({[key]: node[key]})
        if (Array.isArray(node[key])) node[key].forEach((i) => stack.push(i))
      }
    }
   return res
 }
```
</details>
  
---
  
#### flatten nested object (в плоский объект рекурсивно)  
<details><summary> </summary>

```javascript
 
const flattenObj = (obj) => {
  let res = {}
  for (let key in obj) {
    if (typeof obj[key] === 'object' && obj[key]!==null) {
      res = {...res, ...flattenObj(obj[key])}
    } else {
      res[key] = obj[key]
    }
  }
  return res
}
```
</details>
  
---

#### всяко разно  
  
```javascript
let a = {};
let b = { key: 'test' };
let c = { key: 'test' };

a[b] = '123';
a[c] = '456';

console.log(a);
```
<details><summary> </summary>

```javascript
 {
   [object Object]: "456"
}
```
</details>
  
---

```javascript

function Pet(name) {
 this.name = name;
 this.getName = () => this.name;
}
const cat = new Pet('Fluffy');
console.log(cat.getName()); 
const { getName } = cat;
console.log(getName());
  
```

```javascript

const object = {
  who: 'World',
  greet() {
    return `Hello, ${this.who}!`;
},
  farewell: () => {
    `Goodbye, ${this.who}!`;
  }
};

console.log(object.greet()); 
console.log(object.farewell()); 
  
```

```javascript
var length = 4;

function callback() {
 console.log(this.length); 
}

const object = {
  length: 5,
  method(callback) {
  callback();
}
};

object.method(callback);
```
