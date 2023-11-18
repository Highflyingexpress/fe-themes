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
 * const b = [2,3,5];
 * merge(a, b);  // [1,2,3,3,4,5]
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
  
