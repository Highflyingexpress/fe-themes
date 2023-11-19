#### [Promise hell](promisehell.md)  

  
#### создать массив от 0 до 9

```
данных нет, создаем массив из ничего
```
<details><summary> </summary>
  
```javascript
let arr = Array.from({length:10}).map((v,k)=>k)
```
</details>
  
---
  
#### отсортировать массив по частоте появления

```javascript

const foo = (arr) => {}
console.log(foo([1,1,1,2,2,2,2,4,4,5,0])) // [2,1,4,5,0]
```
<details><summary> </summary>
  
```javascript
  const foo = (arr) => {
   let obj = {}
   for (let item of arr) {
     obj[item] = (obj[item] ?? 0) + 1
   }
   return Object.entries(obj).sort((a,b)=>b[1]-a[1]).reduce((acc,item)=>{
     acc.push(item[0])
     return acc
   },[])
 }
```
  
</details>
  
---

#### сжатие(сворачивание) строки

```javascript

// сжатие(сворачивание) строки - символ кол-во повторений, символ кол-во повторений ...
const foo = (arr) => {}
console.log(foo('111122234411155522266')) // "142331421353236"
```
<details><summary> </summary>
  
```javascript
  const foo = (str) => {
  let res = str[0];
  let count = 1;
  let j = 0;
  for (let i=1; i < str.length; i++) {
    if (str[i]===str[i-1]) { count++ }
    else {
      res+=String(count);
      res+=String(str[i]);
      count=1;
    }
  }
  return res
}
```
  
</details>
  
---
  
#### плющим массив без рекурсии
  
```javascript  

function flatten(arr) {}
console.log(flatten([[1], [[2, 3]], [[[4]]]])); // -> [1, 2, 3, 4]
```
<details><summary> </summary>
  
```javascript
// без рекурсии
const flatten = (arr) => {
  let res = [...arr];
  let i = 0;
  while (i < res.length) {
    if (Array.isArray(res[i])) {
      res.splice(i, 1, ...res[i])
    }
    else i++
  }
  return res
}
```
</details>
  
---
  
#### объединить два отсортированных массива в один отсортированный  

```
 const a = [1,3,4];
 const b = [2,3,5];
 merge(a, b);  // [1,2,3,3,4,5]
```
  
<details><summary> </summary>

```javascript
  function merge(a, b) {
    let i = a.length - 1;
    let j = b.length - 1;
    let end = a.length + b.length - 1;
    
    while (j >= 0) {
      if (i >= 0 && a[i] > b[j]) {
        a[end] = a[i];
        i--;
      } else {
        a[end] = b[j];
        j--;
      }
      end--;
    }
    return a
}
```
</details>
  
---
  
#### повернутый палиндром  

```
CBAABCD это повернутый палиндром ABCDCBA.
BAABCC это повернутый палиндром ABCCBA
```
  
---
  
#### валидация скоб

```javascript
function isBalanced(str) {}

console.log(isBalanced("(x + y) - (4)")); // -> true
console.log(isBalanced("(((10 ) ()) ((?)(:)))")); // -> true
console.log(isBalanced("[({()})]")); // -> true
console.log(isBalanced("(50)((")); // -> false
```
<details><summary> </summary>
```javascript
  function isBalanced(str) {
  let stack = []
  let braces = {
    '{':'}',
    '[':']',
    '(':')',
  }
  let bracesArr = Object.keys(braces).join('') + Object.values(braces).join('')
  console.log(bracesArr)
  for (let char of str) {
    if (bracesArr.includes(char)) {
     if (braces[char]) stack.push(char) // открытая
      else {
        if (braces[stack.pop()] !== char ) return false
      }
    }
  }
  if (stack.length) return false
  else return true
}
```
</details>
  
---

#### мемоизация вызова ф-ции 
  
```javascript
const memo = (fn) => {}

const plus = (a, b, c) => {
  console.log('plus', a, b, c)
  return a + b + c
}

const divide = (a, b) => {
  console.log('divide', a, b)
  return a / b
} 

const memoPlus = memo(plus)
console.log(memoPlus(1, 2, 3)) // plus 1, 2, 3 -> 6
console.log(memoPlus(3, 1, 1)) // plus 3, 1, 1 -> 5
console.log(memoPlus(1, 2, 3)) // 6

const memoDivide = memo(divide)
console.log(memoDivide(4, 2)) // divide 4, 2 -> 2
console.log(memoDivide(6, 2)) // divide 6, 2 -> 3
console.log(memoDivide(4, 2)) // 2
```

<details><summary> </summary>

```javascript
 const memo = (fn) => {
  let cache = {}
  return function(...args) {
    if (cache[args]) return cache[args]
    else { 
      cache[args] = fn(...args)
      return cache[args]
    }
  }
}
```
  
</details>
  
---
  
#### chaining

```javascript
const obj = {
  a: {
    b: {
      c: {
        d: "Привет!",
      },
    },
  },
};


const optionalChaining = (o, path) => {}
console.log(optionalChaining(obj, "a.b.c")); // Ответ = { d: 'Привет' }
console.log(optionalChaining(obj, "a.b.c.d")); // Ответ = Привет
console.log(optionalChaining(obj, "a.b.c.d.e")); // Ответ = undefined
console.log(optionalChaining(obj, "b.d.a")); // Ответ = undefined
console.log(optionalChaining(obj, "")); /* Ответ = {
//   a: {
//     b: {
//       c: {
//         d: 'Привет!',
//       },
//     },
//   },
// } 
// */
```
<details><summary> </summary>

```javascript
  const optionalChaining = (o, path) => {
  if (!path.length) return o;
  
  let paths = path.split('.')
  let obj = {...o}
             
  for (let chain of paths) {
    if (obj[chain]) obj = obj[chain] 
    else return undefined
  }
  return obj
}
```
  
</details>
  
---
  
#### carry

```javascript
 f(3)(4) // 7 карри изи
 f(1,6)(8)() // общий карри
```
  
<details><summary> </summary>

```javascript
  function sum(...args) {
  if (!args.length) return 0
  let res = args.reduce((a,b)=>a+b)
  return function inner(...nextArgs) {
    if(!nextArgs.length) return res 
    else return sum(res, ...nextArgs)
  }
}

console.log( sum(1,5)(2)() ); // 8

// изи
// function sum(a, b) {
//   if (b===undefined) {
//     return function inner(c) {
//       return a+c
//     }
//   }
//   else return a+b
// }

// console.log(sum(5,4))
// console.log(sum(5)(4))
```
  
</details>
  
---
  
#### сумма всех age в {{...}}

```javascript
function sumAge(user) {}

const user1 = {
    name: 'Петр',
    age: 49,
    children: [
        {
            name: 'Нина',
            age: 25,
            children: [
                {
                    name: 'Андрей',
                    age: 3,
                },
                {
                    name: 'Олег',
                    age: 1,
                }
          ]
        },
        {
            name: 'Александр',
            age: 22,
        }
    ]
}

console.log(sumAge(user1)) // 100
```

<details><summary> </summary>

```javascript
  function sumAge(user) {
    let res = 0;
    let stack = [user]
    while (stack.length) {
      let obj = stack.pop()
        for (let key in obj) {
          if (key ==='age') res += obj['age']
          if (Array.isArray(obj[key])) stack.push(...obj[key])
        }
    }
    return res
  }
```
  
</details>

#### bankomat  

```javascript
const bancomat = (money) => {};
//доступные купюры 100, 50, 20, 10
console.log(bancomat(280)); // [100, 100, 50, 20, 10]
```

<details><summary> </summary>
  
```javascript
// классическая задача
const bancomat = (money) => {
  return [100, 50, 20, 10].reduce((acc, coin) => {
    while(coin<=money) {
      acc.push(coin)
      money-=coin
    }
    return acc
  }, [])
};

// задача, где нужно выводить объект каких купюр сколько

const bancomat = (price, arr) => {
 res = {}
 for (let coin of arr) {
   count = Math.floor(price / coin)
   price -= count*coin
   res[coin] = count
 }
  return res
};

```
</details>
  
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

```
</details>
  
---

#### Из исходного массива сделать объект, ключами которого будут все встречающиеся gender, а значениями массив объектов юзеров
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

