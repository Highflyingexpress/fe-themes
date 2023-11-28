<img src="https://github.com/Highflyingexpress/fe-themes/assets/107925514/a9ea18d2-b59d-473d-8130-aa545b7ef6e6" width="500">  
  
```javascript
import {unstable_batchedUpdates} from 'react-dom';

const batchUpdate = unstable_batchedUpdates(() => {
  setName('Moustafa');
  setAge(25);
});


batchUpdate() //this will group all state changes inside and apply it in one re-render
```  
   
