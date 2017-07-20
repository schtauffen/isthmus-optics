# @isthmus/optics
This is a small set of optics for modifying objects in an immutable fashion.

## Installation
You can install _@isthmus/optics with:
```
npm install --save @isthmus/optics
```

Then to use in your JavaScript:
```js
import { set, view, over } from '@isthmus/atom'

// and then use...
```

There is a umd version available under `@isthmus/optics/dist/optics.js`:
```html
<script src="https//unpkg.com/@isthmus/optics/dist/optics.js"></script>
<script>
  const { set, view, over } = isthmusOptics
  // ...
</script>
```

## API
Note that all functions without optional arguments are curried with `crry`. 
  * [set](#set)
  * [view](#view)
  * [over](#over)

### set
> set(lens, value, target) -> result  

`set` is a function which takes a lens (string, number, or array), value, and object or array. It makes the adjustment and returns the result.   
The original target is not modified.  
```js
const obj = { a: 'foo', b: [1, 2, 3] }
const arr = [1, 2, 3]

set('a', 'bar', obj) // { a: 'bar', b: [1, 2, 3] }
set(1, 7, arr) // [1, 7, 3]
set(['b', 1], 11, obj) // { a: 'foo', b: [1, 11, 3] }
```

### view
> view(lens, target) -> result  

`view` is a function which takes a lens and target. It returns the result if it is found, or `undefined` otherwise.
```js
const obj = { a: 'foo', b: [1, 2, 3] }

view('a', obj) // 'foo'
view(['b', 1], obj) // 2
view(['c', 7, 'd'], obj) // undefined
```

### over
> over(lens, transform, target) -> result  

`over` is a function which takes a lens, transform function, and object. It adjusts the target based on the given transform, and returns the result.   
The original target is not modified.  
```js
const obj = { a: 'foo', b: [1, 2, 3] }

over(['b', 1], x => x * x, obj) // { a: 'foo', b: [1, 4, 3] }
```
