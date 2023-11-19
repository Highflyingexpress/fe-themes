```javascript
function a() { 
  console.log('1') 
  Promise.resolve().then(a) 
} 
 
function b() { 
  console.log('2') 
  setTimeout(b); 
} 
a() 
b()
```
  
---  

```javascript
console.log('start');

const promise1 = new Promise((resolve, reject) => {
  console.log(1)
})

console.log('end');
```
  
---  

```javascript
console.log('start');

const promise1 = new Promise((resolve, reject) => {
  console.log(1)
  resolve(2)
})

promise1.then(res => {
  console.log(res)
})

console.log('end');
```
 
---  

```javascript

  
