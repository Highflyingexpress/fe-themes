```javascript
// отсортировать по частоте появления
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

```javascript
  
---
  
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
  

```javascript  
// плоский массив
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
  

