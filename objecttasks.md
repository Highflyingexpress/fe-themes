## Задачки с объектами
  
---
  
#### что выведет в консоль
  
```
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
  
---
  
#### Написать функцию, которая суммирует все значения дерева. Нужно решить задачу без использования рекурсии. Вложенность объекта может быть любая  
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
    if (obj['gender']) {
      let {gender, ...rest} = obj
      if (returnObj[gender]) { 
        returnObj[gender].push(rest)
      }
      else returnObj[gender] = [rest] 
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
