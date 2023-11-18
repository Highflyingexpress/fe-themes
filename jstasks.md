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
