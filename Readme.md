Q1. What is shallow & deep copy? How can we do shallow and deep copy in objects?

    A shallow copy of an object produces a new object, but its properties still refer to the properties of the original object. Consequently, modifications to nested objects or arrays within the copied object will impact the original object, and vice versa. In JavaScript, several methods can be used to create a shallow copy, including Object.assign(), the spread operator (...), or the Array.slice() method.
```js
const originalObj = { a: 1, b: { c: 2 } };
const shallowCopy = Object.assign({}, originalObj);

console.log(shallowCopy); // Output: { a: 1, b: { c: 2 } }

shallowCopy.a = 99;
shallowCopy.b.c = 88;

console.log(originalObj); // Output: { a: 1, b: { c: 88 } }

```
    On the other hand, a deep copy of an object generates an entirely independent duplicate of the original object, along with all its nested objects or arrays. Any changes made to the copied object's properties will have no effect on the original object. 
```js
const originalObj = { a: 1, b: { c: 2 } };
const deepCopy = JSON.parse(JSON.stringify(originalObj));

console.log(deepCopy); // Output: { a: 1, b: { c: 2 } }

deepCopy.a = 99;
deepCopy.b.c = 88;

console.log(originalObj); // Output: { a: 1, b: { c: 2 } }

```
Q2. What will be the output?Why?
```js
function sum(...theArgs) { 
    return theArgs.reduce((previous, current) => { 
         return previous + current; }); 
     } 
console.log(sum(1, 2, 3)); 
console.log(sum(1, 2, 3, 4));

Output : 
6
10
```

    In the function sum we are using rest operator in parameter for taking inputs as we are unaware of number of arguments so all the arguments are received as in one array name "theArgs" and we the using reduce method of arrays to add all the value in array and then return the sum.

Q3. What will be the output?Why?
```js
function addition(number1, number2, number3) { 
  console.log(number1 + number2 + number3); 
} 
let numbers = [10, 20, 30]; 
addition(...numbers);

Output : 
60
```

    The addition function takes three parameters (number1, number2, and number3) and logs the sum of these three numbers to the console. When calling the addition function with the spread operator (...), the elements of the numbers array are passed as individual arguments to the function. So, it's equivalent to calling addition(10, 20, 30). The function then calculates the sum of these three numbers (10 + 20 + 30) and logs 60 to the console.

Q4. What is the difference between object and map?

    In JS, an object is a collection of key-value pairs where keys are strings or symbols, and values can be of any data type (including other objects or functions) But Thats not enough for Real world scenario keys are not always just string so thats why maps exist. Maps also store key-value pairs but the keys can be of any datatype even objects,sets,maps can also be key. 

    For example : 
```js

const obj = {
    key:"value"
    }
const arr=[1,2];
obj[arr]=1;
obj.arr=2;
const map=new Map();
map.set(arr,1);
console.log(map);
console.log(obj)

```

obj[arr] = 1;

    In JS, when you use an object as a key, it is automatically converted to a string. In this case, the array arr is converted to a string, which results in the string "1,2". So, this line adds a new property to the obj with the key "1,2" and the value 1. Now, the object obj looks like this: { key: "value", "1,2": 1 }.
    
obj.arr = 2;

    This adds a new property to the obj with the key "arr" and the value 2. Now, the object obj looks like this: { key: "value", "1,2": 1, arr: 2 }.

const map = new Map();
    This creates a new Map named map.

map.set(arr, 1);

    Here, we use the array arr as the key in the Map. Unlike objects, Maps in JavaScript can use complex objects (like arrays) as keys without any implicit conversion. So, we set the value 1 for the key arr in the Map.

console.log(map);
console.log(obj);

Output: 
```js
    Map(1) { [ 1, 2 ] => 1 }
    { key: 'value', '1,2': 1, arr: 2 }

```

Q5. Rewrite the code below to use array destructuring instead of assigning each value to a variable.
    let item = ["Egg", 0.25, 12]; 
    let name = item[0]; 
    let price = item[1]; 
    let quantity = item[2]; 
    console.log(`Item: ${name}, Quantity: ${quantity}, Price: ${price}`);


```js
let item = ["Egg", 0.25, 12]; 
let [Item_name,price,quantity]=item;
console.log(`Item: ${Item_name}, Quantity: ${quantity}, Price: ${price}`);

Output:
Item: Egg, Quantity: 0.25, Price: 12
```

Q6. Using Array Destructuring get all of the names from this Nested Array

```js
const moreStudents = [ 'Chris', ['Ahmad', 'Antigoni'], ['Toby', 'Sam'] ]; 
// Write your code here 
const [student1,[student2,student3],[student4,student5]] = moreStudents; 
console.log(student1, student2, student3, student4, student5);
    
Output:
Chris Ahmad Antigoni Toby Sam

```
Q7. Fix the code to make it work.

```js
let map = new Map();
map.set("key", "value");
let keys = map.keys();
let moreKeys = Array.from(keys);
moreKeys.push("more");
```
    code will not work because the keys variable is an iterable, not an array.
    we cannot use array methods on an iterable. To fix the code, we need to convert the keys variable to an array.

    Array.from() method: create a new array called moreKeys that contains all of the keys from the keys iterable, plus we now use push to add "more" in moreKeys.

Corrected code:
```js
let map = new Map();
map.set("key", "value");
let keys = map.keys();
let moreKeys = Array.from(keys);
moreKeys.push("more");

console.log(moreKeys);

Output :
["key", "more"]
```
---

Q8. What is the difference between set and weakset? Explain with the help of examples.

    *Set stores the unique values of any datatype but weaksets can only stores the objects.
    *Sets can prevent elements from being garbage collected as long as they are part of the Set. But In weaksets it stores the weak references of object so if object reference is deleted from any other mean in the program it also deleted from the weaksets. 
    *Sets are iteratable but weaksets cannot be iterated over. It only has add, delete, and has methods.

    ```js
let weakSet = new WeakSet();
let set = new Set();
let obj1 = { name: "Shubham" };
let obj2 = { name: "Jain" };

weakSet.add(obj1);
weakSet.add(obj2);
console.log(weakSet);
set.add(obj1);
set.add(obj2);
console.log(weakSet.has(obj1)); // Output: true

obj1 = null; // Removing the strong reference to obj1

// At this point, obj1 has no strong reference, so it is garbage collected
// WeakSet won't prevent the cleanup of obj1

console.log(weakSet.has(obj1)); // Output: false
console.log(weakSet.has(obj2)); // Output: true
console.log(set); //Set(2) { { name: 'Shubham' }, { name: 'Jain' } }
    
    
 ```

Q9. What is the difference between map and weakmap? Explain with the help of examples.

    *Map stores the unique Key-values pairs of any datatype but weakMaps can only stores the objects as keys.
    *Maps can prevent elements from being garbage collected as long as they are part of the Map. But In weakMap it stores the weak references of object(keys) so if object reference is deleted from any other mean in the program it also delete that key-value pair from the weakmaps. 
    *Maps are iteratable but weakmaps cannot be iterated over. It only has add, delete, get and has methods.

    ```js
let weakmap = new WeakMap();
let map = new Map();
let obj1 = { name: "Shubham" };
let obj2 = { name: "Jain" };

weakMap.set(obj1,"s);
weakMap.set(obj2,"j);
console.log(weakSet);
map.set(obj1,"s);
map.set(obj2,"j);
console.log(weakmap.has(obj1)); // Output: true

obj1 = null; // Removing the strong reference to obj1

// At this point, obj1 has no strong reference, so it is garbage collected
// WeakSet won't prevent the cleanup of obj1

console.log(weakSet.has(obj1)); // Output: false
console.log(weakSet.has(obj2)); // Output: true
console.log(map); //Map(2) { { name: 'Shubham' } => 's', { name: 'Jain' } => 'j' }
    
    
 ```



