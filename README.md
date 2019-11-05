# Javascript Interview Cheat Sheet

## Table of Contents

 1. [Datatypes](#datatypes)
 1. [Variables](#variables)
 1. [Objects](#objects)
 1. [Strings](#strings)
 1. [Arrays](#arrays)
 1. [Maps](#maps)
 1. [Sets](#sets)
 1. [Promise](#promise)
 1. [Regular Expressions](#regularexpressions)
 1. [Bitwise Operators](#bitwiseoperators)

---

## Datatypes
JavaScript provides seven different data types:

| Data Types  | Examples                                                              |
| ----------- | --------------------------------------------------------------------- |
| `undefined` | A variable that has not been assigned a value is of type `undefined`. |
| `null`      | no value.                                                             |
| `string`    | `'a', 'aa', 'aaa', 'Hello!', '11 cats'`                               |
| `number`    | `12, -1, 0.4`                                                         |
| `boolean`   | `true, false`                                                         |
| `object`    | A collection of properties.                                           |
| `symbol`    | Represents a unique identifier.                                       |

---

## Variables
In JavaScript (ES6), there are two keywords available to declare a variable, and each has its differences. Those are `let` and `const`.

<table>
  <tr>
    <th></th>
    <th>Scope</th>
    <th>Reassignable</th>
    <th>Mutable</th>
    <th>Temporal Dead Zone</th>
  </tr>
  <tr>
    <th>const</th>
    <td>Block</td>
    <td>No</td>
    <td>Yes*</td>
    <td>Yes</td>
  </tr>
  <tr>
    <th>let</th>
    <td>Block</td>
    <td>Yes</td>
    <td>Yes</td>
    <td>Yes</td>
  </tr>
</table>

💡**NOTE**: *object* and *array* ```const``` declared variables **can** be mutated.

### Sample code

```javascript
const person = "Nick";
person = "John" // Will raise an error, person can't be reassigned
```

```javascript
let person = "Nick";
person = "John";
console.log(person) // "John", reassignment is allowed with let
```

---

## Objects
The Object constructor creates an object wrapper for the given value. If the value is null or undefined, it will create and return an empty object, otherwise, it will return an object of a Type that corresponds to the given value.

```javascript
const cat = {
  name: "Whiskers",
  legs: 4,
  tails: 1,
  enemies: ["Water", "Dogs"]
};
```

### Basics

To access nested objects:
```javascript
const ourStorage = {
  desk: {
    drawer: "stapler"
  },
  cabinet: {
    "top drawer": {
      folder1: "a file",
      folder2: "secrets"
    },
    "bottom drawer": "soda"
  }
};

ourStorage.cabinet["top drawer"].folder2; // "secrets"
ourStorage.desk.drawer; // "stapler"
```

#### Destructuring Object Variables

```javascript
// Consider the following ES5 code
const voxel = { x: 3.6, y: 7.4, z: 6.54 };
let x = voxel.x; // x = 3.6
let y = voxel.y; // y = 7.4
let z = voxel.z; // z = 6.54

// the same assignment statement with ES6 destructuring syntax
const { x, y, z } = voxel; // x = 3.6, y = 7.4, z = 6.54

// to store the values of voxel.x into a, voxel.y into b, and voxel.z into c, you have that freedom as well
const { x: a, y: b, z: c } = voxel; // a = 3.6, b = 7.4, c = 6.54

// Destructuring Variables from Nested Objects
const a = {
  start: { x: 5, y: 6 },
  end: { x: 6, y: -9 }
};

const {
  start: { x: startX, y: startY }
} = a;

console.log(startX, startY); // 5, 6
```

### Object Methods

#### `Object.keys()`
The `Object.keys()` method returns an array of a given object's own enumerable property names, in the same order as we get with a normal loop.

```javascript
const object1 = {
  a: 'somestring',
  b: 42,
  c: false
};

console.log(Object.keys(object1));
// expected output: Array ["a", "b", "c"]
```

#### `Object.entries()`
The `Object.entries()` method returns an array of a given object's own enumerable string-keyed property `[key, value]` pairs

```javascript
const object1 = {
  a: 'somestring',
  b: 42
};

for (let [key, value] of Object.entries(object1)) {
  console.log(`${key}: ${value}`);
}

// expected output:
// "a: somestring"
// "b: 42"
// order is not guaranteed
```

#### `Object.hasOwnProperty()`
The `hasOwnProperty()` method returns a boolean indicating whether the object has the specified property as its own property (as opposed to inheriting it).

```javascript
const myObj = {
  top: "hat",
  bottom: "pants"
};

myObj.hasOwnProperty("top"); // true
myObj.hasOwnProperty("middle"); // false
```

---

## Strings

### Basics

```javascript
// escape literal quotes
let sampleStr = 'Alan said, "Peter is learning JavaScript".';
// this prints: Alan said, "Peter is learning JavaScript".

// concatenating strings
let ourStr = "I come first. " + "I come second.";

// concatenating strings with +=
let ourStr = "I come first. ";
ourStr += "I come second.";

// constructing strings with variables
let ourName = "freeCodeCamp";
let ourStr = "Hello, our name is " + ourName + ", how are you?";

// appending variables to strings
let anAdjective = "awesome!";
let ourStr = "freeCodeCamp is ";
ourStr += anAdjective;
```

### Escape sequences

| Code | Output             |
| ---- | ------------------ |
| `\'` | single quote (`'`) |
| `\"` | double quote (`"`) |
| `\\` | backslash (`\`)    |
| `\n` | newline            |
| `\r` | carriage return    |
| `\t` | tab                |
| `\b` | backspace          |
| `\f` | form feed          |

### ES6 Template Literals

```javascript
const person = {
  name: "Zodiac Hasbro",
  age: 56
};

// Template literal with multi-line and string interpolation
const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting);
// Hello, my name is Zodiac Hasbro!
// I am 56 years old.
```

### String Methods

#### `length`
Reflects the length of the string.
```javascript
"Adam Espi".length; // 9
```

#### `includes()`
The `includes()` method determines whether one string may be found within another string, returning `true` or `false` as appropriate.

```javascript
let sentence = 'The quick brown fox jumps over the lazy dog.';

let word = 'fox';

console.log(`The word "${word}" ${sentence.includes(word)? 'is' : 'is not'} in the sentence`);
// expected output: "The word "fox" is in the sentence"
```

#### `indexOf()`
The `indexOf()` method returns the index within the calling String object of the first occurrence of the specified value, starting the search at `fromIndex`. Returns `-1` if the value is not found.

```javascript
let paragraph = 'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?';

let searchTerm = 'dog';
let indexOfFirst = paragraph.indexOf(searchTerm);

console.log('The index of the first "' + searchTerm + '" from the beginning is ' + indexOfFirst);
// expected output: "The index of the first "dog" from the beginning is 40"

console.log('The index of the 2nd "' + searchTerm + '" is ' + paragraph.indexOf(searchTerm, (indexOfFirst + 1)));
// expected output: "The index of the 2nd "dog" is 52"
```

#### `replace()`
The `replace()` method returns a new string with some or all matches of a pattern replaced by a replacement. If pattern is a string, only the first occurrence will be replaced.

```javascript
let p = 'The quick brown fox jumps over the lazy dog. If the dog reacted, was it really lazy?';

let regex = /dog/gi;

console.log(p.replace(regex, 'ferret'));
// expected output: "The quick brown fox jumps over the lazy ferret. If the ferret reacted, was it really lazy?"

console.log(p.replace('dog', 'monkey'));
// expected output: "The quick brown fox jumps over the lazy monkey. If the dog reacted, was it really lazy?"
```

#### `slice()`
`slice()` extracts up to but not including `endIndex`. `str.slice(1, 4)` extracts the second character through the fourth character (characters indexed 1, 2, and 3). If negative, it is treated as `strLength + (beginIndex)` where `strLength` is the length of the string (for example, if `beginIndex` is `-3` it is treated as `strLength - 3`).

```javascript
let str = 'The quick brown fox jumps over the lazy dog.';

console.log(str.slice(31));
// expected output: "the lazy dog."

console.log(str.slice(-9, -5));
// expected output: "lazy"

```

#### `split()` and `join()`
`split()` a String object into an array of strings by separating the string into substrings.

```javascript
let str = 'a string';
let splittedStr = str.split('');
// ​​​​​[ 'a', ' ', 's', 't', 'r', 'i', 'n', 'g' ]​​​​​

let joinedStr = splittedStr.join('');
// a string​​​​​
```

#### `startsWith()`
The `startsWith()` method determines whether a string begins with the characters of a specified string, returning `true` or `false` as appropriate.

```javascript
const str1 = 'Saturday night plans';

console.log(str1.startsWith('Sat'));
// expected output: true

console.log(str1.startsWith('Sat', 3));
// expected output: false
```

#### `substring()`
The `substring()` method returns the part of the string between the start and end indexes, or to the end of the string.

```javascript
let str = 'Mozilla';

console.log(str.substring(1, 3));
// expected output: "oz"
```

#### `toLowerCase()`
The `toLowerCase()` method returns the calling string value converted to lower case.

```javascript
let sentence = 'The quick brown fox jumps over the lazy dog.';

console.log(sentence.toLowerCase());
// expected output: "the quick brown fox jumps over the lazy dog."
```

#### `toUpperCase()`
The `toUpperCase()` method returns the calling string value converted to uppercase (the value will be converted to a string if it isn't one).

```javascript
let sentence = 'The quick brown fox jumps over the lazy dog.';

console.log(sentence.toUpperCase());
// expected output: "THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG."
```

---

## Arrays

### Basics

```javascript
const fruits = ['Apple', 'Banana'];

fruits.push('Orange');
// ["Apple", "Banana", "Orange"]
```

### Array Methods
These methods modify the array:

#### `length`
The Array constructor's length property.

```javascript
let last = fruits[fruits.length - 1];
// Banana
```

#### `fill()`
The `fill()` method fills (modifies) all the elements of an array from a start index (default zero) to an end index (default array length) with a static value. It returns the modified array.

If `start` is negative, it is treated as `length+start` where `length` is the length of the array. If `end` is negative, it is treated as `length+end`.

```javascript
let array1 = [1, 2, 3, 4];

// fill with 0 from position 2 until position 4
console.log(array1.fill(0, 2, 4));
// expected output: [1, 2, 0, 0]

// fill with 5 from position 1
console.log(array1.fill(5, 1));
// expected output: [1, 5, 5, 5]

Array(3).fill(4);                // [4, 4, 4]
[].fill.call({ length: 3 }, 4);  // {0: 4, 1: 4, 2: 4, length: 3}

// Objects by reference.
let arr = Array(3).fill({}) // [{}, {}, {}];
arr[0].hi = "hi"; // [{ hi: "hi" }, { hi: "hi" }, { hi: "hi" }]
```

#### `pop()`
The `pop()` method removes the last element from an array and returns that element. This method changes the length of the array.

```javascript
let myFish = ['angel', 'clown', 'mandarin', 'sturgeon'];

let popped = myFish.pop();

console.log(myFish); // ['angel', 'clown', 'mandarin' ]

console.log(popped); // 'sturgeon'
```

#### `push()`
The `push()` method adds one or more elements to the end of an array and returns the new length of the array.

```javascript
let sports = ['soccer', 'baseball'];
sports.push('football', 'swimming');

console.log(sports); // ['soccer', 'baseball', 'football', 'swimming']
```

#### `reverse()`
The `reverse()` method reverses an array in [place](https://en.wikipedia.org/wiki/In-place_algorithm). The first array element becomes the last, and the last array element becomes the first.

```javascript
const a = [1, 2, 3];

console.log(a); // [1, 2, 3]

a.reverse();

console.log(a); // [3, 2, 1]
```

#### `shift()`
The `shift()` method removes the first element from an array and returns that removed element. This method changes the length of the array.

```javascript
const array1 = [1, 2, 3];

const firstElement = array1.shift();

console.log(array1);
// expected output: Array [2, 3]

console.log(firstElement);
// expected output: 1
```

#### `sort()`
The `sort()` method sorts the elements of an array in place and returns the sorted array. The default sort order is built upon converting the elements into strings, then comparing their sequences of UTF-16 code units values.

```javascript
let numbers = [4, 2, 5, 1, 3];
numbers.sort((a, b) => a - b);

console.log(numbers);
// [1, 2, 3, 4, 5]
```

#### `splice()`
The `splice()` method changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.

If greater than the length of the array, start will be set to the length of the array. If `negative`, it will begin that many elements from the end of the array (with origin `-1`, meaning `-n` is the index of the nth last element and is therefore equivalent to the index of `array.length - n`). If the absolute value of start is greater than the length of the array, it will begin from index `0`.

```javascript
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at index 1

console.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'June']

const myFish = ['angel', 'clown', 'trumpet', 'sturgeon'];
const removed = myFish.splice(0, 2, 'parrot', 'anemone', 'blue');

// myFish is ["parrot", "anemone", "blue", "trumpet", "sturgeon"]
// removed is ["angel", "clown"]
```

#### `unshift()`
The `unshift()` method adds one or more elements to the beginning of an array and returns the new length of the array.

```javascript
const array1 = [1, 2, 3];

console.log(array1.unshift(4, 5));
// expected output: 5

console.log(array1);
// expected output: Array [4, 5, 1, 2, 3]
```

### Array Accessors
These methods do not modify the array and return some representation of the array.

#### `includes()`
The `includes()` method determines whether an array includes a certain value among its entries, returning `true` or `false` as appropriate.

```javascript
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// expected output: true
```

#### `join()`
The `join()` method creates and returns a new string by concatenating all of the elements in an array (or an array-like object), separated by commas or a specified separator string.

```javascript
const elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"
```

#### `indexOf()`
The `indexOf()` method returns the first index at which a given element can be found in the array, or `-1` if it is not present.

```javascript
const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

console.log(beasts.indexOf('bison'));
// expected output: 1

// start from index 2
console.log(beasts.indexOf('bison', 2));
// expected output: 4
```

### Array Iterators

#### `map()`
The `map()` method creates **a new array** with the results of calling a provided function on every element in the calling array.

```javascript
var array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

#### `reduce()`
The `reduce()` method executes **a reducer function** (that you provide) on each element of the array, resulting in a single output value.

```javascript
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

Suppose the following use of `reduce()` occurred:

```javascript
[0, 1, 2, 3, 4].reduce(function(accumulator, currentValue, currentIndex, array) {
  return accumulator + currentValue;
});
```

The callback would be invoked four times, with the arguments and return values in each call being as follows:

<table>
 <thead>
  <tr>
   <th scope="col"><code>callback</code></th>
   <th scope="col"><code>accumulator</code></th>
   <th scope="col"><code>currentValue</code></th>
   <th scope="col"><code>currentIndex</code></th>
   <th scope="col"><code>array</code></th>
   <th scope="col">return value</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th scope="row">first call</th>
   <td><code>0</code></td>
   <td><code>1</code></td>
   <td><code>1</code></td>
   <td><code>[0, 1, 2, 3, 4]</code></td>
   <td><code>1</code></td>
  </tr>
  <tr>
   <th scope="row">second call</th>
   <td><code>1</code></td>
   <td><code>2</code></td>
   <td><code>2</code></td>
   <td><code>[0, 1, 2, 3, 4]</code></td>
   <td><code>3</code></td>
  </tr>
  <tr>
   <th scope="row">third call</th>
   <td><code>3</code></td>
   <td><code>3</code></td>
   <td><code>3</code></td>
   <td><code>[0, 1, 2, 3, 4]</code></td>
   <td><code>6</code></td>
  </tr>
  <tr>
   <th scope="row">fourth call</th>
   <td><code>6</code></td>
   <td><code>4</code></td>
   <td><code>4</code></td>
   <td><code>[0, 1, 2, 3, 4]</code></td>
   <td><code>10</code></td>
  </tr>
 </tbody>
</table>

#### `filter()`
The `filter()` method creates **a new array** with all elements that pass the test implemented by the provided function.

```javascript
let words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

### Spread Operator

```javascript
// The ES5 code below uses apply() to compute the maximum value in an array.
var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr); // 89

// ...arr returns an unpacked array. In other words, it spreads the array.
const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr); // 89

// [...new Set(arr)] = unique value array
const arr = [1,2,2,3,3,4,5,5];
const uniq = [...new Set(arr)]; // [1,2,3,4,5]

// copy an array
let thisArray = [true, true, undefined, false, null];
let thatArray = [...thisArray];
// thatArray equals [true, true, undefined, false, null]
// thisArray remains unchanged, and is identical to thatArray

// combine arrays
let thisArray = ['sage', 'rosemary', 'parsley', 'thyme'];
let thatArray = ['basil', 'cilantro', ...thisArray, 'coriander'];
// thatArray now equals ['basil', 'cilantro', 'sage', 'rosemary', 'parsley', 'thyme', 'coriander']
```

---

## Maps

### Basics
The Map object holds key-value pairs and remembers the original insertion order of the keys. Any value (both objects and primitive values) may be used as either a key or a value.

```javascript
let myMap = new Map();

let keyString = 'a string',
    keyObj = {},
    keyFunc = function() {};

// setting the values
myMap.set(keyString, "value associated with 'a string'");
myMap.set(keyObj, 'value associated with keyObj');
myMap.set(keyFunc, 'value associated with keyFunc');

myMap.size; // 3

// getting the values
myMap.get(keyString);    // "value associated with 'a string'"
myMap.get(keyObj);       // "value associated with keyObj"
myMap.get(keyFunc);      // "value associated with keyFunc"

myMap.get('a string');   // "value associated with 'a string'"
                         // because keyString === 'a string'
myMap.get({});           // undefined, because keyObj !== {}
myMap.get(function() {}); // undefined, because keyFunc !== function () {}

```

#### Map Iterators
Maps can be iterated using a `for..of` loop or `forEach()`:

```javascript
const myMap = new Map();
myMap.set(0, 'zero');
myMap.set(1, 'one');
for (let [key, value] of myMap) {
  console.log(key + ' = ' + value);
}
// 0 = zero
// 1 = one

for (let key of myMap.keys()) {
  console.log(key);
}
// 0
// 1

for (let value of myMap.values()) {
  console.log(value);
}
// zero
// one

for (let [key, value] of myMap.entries()) {
  console.log(key + ' = ' + value);
}
// 0 = zero
// 1 = one

myMap.forEach(function(value, key) {
  console.log(key + ' = ' + value);
});
// 0 = zero
// 1 = one
```

#### Relation with Array objects

```javascript
const kvArray = [['key1', 'value1'], ['key2', 'value2']];

// Use the regular Map constructor to transform a 2D key-value Array into a map
const myMap = new Map(kvArray);

myMap.get('key1'); // returns "value1"

// Use the Array.from function to transform a map into a 2D key-value Array
console.log(Array.from(myMap)); // Will show you exactly the same Array as kvArray

// A more succinct way to do the same with spread syntax
console.log([...myMap]);
```

### Map Methods

#### `clear()`
The `clear()` method removes all elements from a `Map` object.

```javascript
var map1 = new Map();

map1.set('bar', 'baz');
map1.set(1, 'foo');

console.log(map1.size);
// expected output: 2

map1.clear();

console.log(map1.size);
// expected output: 0
```

#### `delete()`
The `delete()` method removes the specified element from a `Map` object by key.


```javascript
let map1 = new Map();
map1.set('bar', 'foo');

console.log(map1.delete('bar'));
// expected result: true
// (true indicates successful removal)

console.log(map1.has('bar'));
// expected result: false

```

#### `get()`
The `get()` method returns a specified element from a `Map` object.

```javascript
let map1 = new Map();
map1.set('bar', 'foo');

console.log(map1.get('bar'));
// expected output: "foo"
```

#### `has()`
The `has()` method returns a boolean indicating whether an element with the specified key exists or not.

```javascript
var map1 = new Map();
map1.set('bar', 'foo');

console.log(map1.has('bar'));
// expected output: true
```

#### `keys()`
The `keys()` method returns a new `Iterator` object that contains the keys for each element in the Map object in insertion order.

```javascript
var myMap = new Map();
myMap.set('0', 'foo');
myMap.set(1, 'bar');
myMap.set({}, 'baz');

var mapIter = myMap.keys();

console.log(mapIter.next().value); // "0"
console.log(mapIter.next().value); // 1
console.log(mapIter.next().value); // Object
```

#### `values()`
he `values()` method returns a new Iterator object that contains the values for each element in the `Map` object in insertion order.

```javascript
var myMap = new Map();
myMap.set('0', 'foo');
myMap.set(1, 'bar');
myMap.set({}, 'baz');

var mapIter = myMap.values();

console.log(mapIter.next().value); // "foo"
console.log(mapIter.next().value); // "bar"
console.log(mapIter.next().value); // "baz"
```

---

## Sets

### Basics
`Set` objects are collections of values. You can iterate through the elements of a set in insertion order. A value in the `Set` **may only occur once**; it is unique in the `Set`'s collection.

```javascript
const set1 = new Set([1, 2, 3, 4, 5]);

console.log(set1.has(1));
// expected output: true

console.log(set1.has(6));
// expected output: false

console.log(set1.size);
// expected output: 6
```

#### Set Iterators

```javascript
// iterate over items in set
// logs the items in the order: 1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
for (let item of mySet) console.log(item);

// Iterate set entries with forEach
mySet.forEach(function(value) {
  console.log(value);
});

[...item].map(index => console.log(index));
// logs the items in the order: 1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
```

#### Relation to Array objects

```javascript
const myArray = ['value1', 'value2', 'value3'];

// Use the regular Set constructor to transform an Array into a Set
const mySet = new Set(myArray);

mySet.has('value1'); // returns true

// Use the spread operator to transform a set into an Array.
console.log([...mySet]); // Will show you exactly the same Array as myArray
```

#### Remove Duplicate from Arrays

```javascript
// Use to remove duplicate elements from the array

const numbers = [2,3,4,4,2,3,3,4,4,5,5,6,6,7,5,32,3,4,5]

console.log([...new Set(numbers)])

// [2, 3, 4, 5, 6, 7, 32]
```

### Set Methods

#### `add()`
The `add()` method appends a new element with a specified value to the end of a Set object.

```javascript
const set1 = new Set();

set1.add(42);
set1.add(42);
set1.add(13);

for (let item of set1) {
  console.log(item);
  // expected output: 42
  // expected output: 13
}
```

#### `clear()`
The `clear()` method removes all elements from a Set object.

```javascript
const set1 = new Set();
set1.add(1);
set1.add('foo');

console.log(set1.size);
// expected output: 2

set1.clear();

console.log(set1.size);
// expected output: 0
```

#### `delete()`
The `delete()` method removes the specified element from a Set object.

```JavaScript
const set1 = new Set();
set1.add({x: 10, y: 20}).add({x: 20, y: 30});

// Delete any point with `x > 10`.
[...set1].forEach(point => {
  if (point.x > 10) {
    set1.delete(point);
  }
});

console.log(set1.size);
// expected output: 1

```

#### `has()`
The `has()` method returns a `boolean` indicating whether an element with the specified value exists in a `Set` object or not.

```javascript
const set1 = new Set([1, 2, 3, 4, 5]);

console.log(set1.has(1));
// expected output: true
console.log(set1.has(6));
// expected output: false
```

#### `keys()` or `values()`
`keys()` the same function as the `values()` function and returns a new `Iterator` object that contains the values for each element in the `Set` object in insertion order.

```javascript
// logs the items in the order: 1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
for (let item of mySet.keys()) console.log(item);

// logs the items in the order: 1, "some text", {"a": 1, "b": 2}, {"a": 1, "b": 2}
for (let item of mySet.values()) console.log(item);
```

---

## Promise

#### Basics
The `Promise` object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.

```javascript
let promise1 = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve('foo');
  }, 300);
});

promise1.then(function(value) {
  console.log(value);
  // expected output: "foo"
});

console.log(promise1);
// expected output: [object Promise]
```

---

## Regular Expressions (Regex)

| Character  | Description                                                                                        |
| ---------- | -------------------------------------------------------------------------------------------------- |
| `\`        | Escapes a special character.                                                                       |
| `|`        | Search for multiple patterns. To match "yes" or "no", the regex is `/yes | no/`.                   |
| `i`        | This flag is used to ignore upper and lowercase. `/ignorecase/i`.                                  |
| `g`        | Search or extract a pattern more than once.                                                        |
| `.`        | The wildcard character `.` will match any character except new lines.                              |
| `[]`       | Allow you to define the characters to match. `/b[au]g/` will match "bag", "bug" but not "bog".     |
| `[a-z]`    | Match all the characters between a and z.                                                          |
| `[1-9]`    | Match all the numbers between 1 and 9.                                                             |
| `[a-z1-9]` | Match all the character between a and z, and the numbers between 1 and 9.                          |
| `[^]`      | Match the characters not in the set. `[^a-e]` match all other characters except A, B, C, D, and E. |
| `+`        | Match 1 or more occurrences of the previous character in a row.                                    |
| `*`        | Match 0 or more occurrences of the previous character.                                             |
| `?`        | Match 0 or 1 occurrence of the previous character. Useful for Lazy matching.                       |
| `^`        | Search for patterns at the beginning of strings.                                                   |
| `$`        | Search for patterns at the end of a string.                                                        |
| `\w`       | Equal to `[A-Za-z0-9_]`. Matches upper, lowercase, numbers the and underscore character (-).       |
| `\W`       | Matches any nonword character. Equivalent to `[^a-za-z0-9_]`.                                      |
| `\d`       | Equal to `[0-9]`. Match one digit.                                                                 |
| `\D`       | Equal to `[^0-9]`. Match one non digit.                                                            |
| `\s`       | Match a whitespace.                                                                                |
| `\S`       | Match everything except whitespace.                                                                |
| `a{2,5}`   | Match the letter `a` between 3 and 5 times.                                                        |
| `a{2,}`    | Specify only the lower number of matches.                                                          |
| `a{5}`     | Specify the exact number of matches.                                                               |
| `(...)`    | Specify a group that can be acceded with number (from 1)                                           |

### Regex Methods

| Method      | Description                                                 |
| ----------- | ----------------------------------------------------------- |
| `test()`    | Returns true or false if the pattern match a string or not. |
| `match()`   | Extract the actual matches found.                           |
| `replace()` | Search and replace text in a string .                       |

### Examples

```javascript
// test method returns true or false if the pattern match a string or not
let myString = "Hello, World!";
let myRegex = /Hello/;
let result = myRegex.test(myString);

// extract the matches of a regex with the match method
let extractStr = "Extract the word 'coding' from this string.";
let codingRegex = /coding/;
let result = extractStr.match(codingRegex);

// Search and replace
let wrongText = "The sky is silver.";
let silverRegex = /silver/;
wrongText.replace(silverRegex, "blue"); // Returns "The sky is blue."

// search for multiple patterns using the alternation or OR operator: |
let petString = "James has a pet cat.";
let petRegex = /dog|cat|bird|fish/;
let result = petRegex.test(petString);

// ignore upper or lowercase
let myString = "freeCodeCamp";
let fccRegex = /freeCodeCamp/i; // flag i
let result = fccRegex.test(myString);

// Search or extract a pattern more than once
let twinkleStar = "Twinkle, twinkle, little star";
let starRegex = /Twinkle/gi; // a regex can have multiple flags
let result = twinkleStar.match(starRegex);

// The wildcard character . will match any character except new lines.
let exampleStr = "Let's have fun with regular expressions!";
let unRegex = /.un/;
let result = unRegex.test(exampleStr);

// define the characters to match, in this example all the vowels in quoteSample
let quoteSample =
  "Beware of bugs in the above code; I have only proved it correct, not tried it.";
let vowelRegex = /[aeiou]/gi;
let result = quoteSample.match(vowelRegex);

// Match all the characters in quoteSample (between a and z)
let quoteSample = "The quick brown fox jumps over the lazy dog.";
let alphabetRegex = /[a-z]/gi;
let result = quoteSample.match(alphabetRegex);

// Match all the character between two characters and numbers
let quoteSample = "Blueberry 3.141592653s are delicious.";
let myRegex = /[h-s2-6]/gi;
let result = quoteSample.match(myRegex);

// Match all that is not a number or a vowel
let quoteSample = "3 blind mice.";
let myRegex = /[^aeiou0-9]/gi;
let result = quoteSample.match(myRegex);

// Match 1 or more occurrences of the previous character (* for 0 or more)
let difficultSpelling = "Mississippi";
let myRegex = /s+/g;
let result = difficultSpelling.match(myRegex);

// ? Match 0 or 1 occurrence of the previous character. Useful for Lazy matching
let text = "titanic";
let myRegex = /t[a-z]*?i/;
let result = text.match(myRegex);

// Search for patterns at the beginning of strings
let rickyAndCal = "Cal and Ricky both like racing.";
let calRegex = /^Cal/;
let result = calRegex.test(rickyAndCal);

// Search for patterns at the end of a string
let caboose = "The last car on a train is the caboose";
let lastRegex = /caboose$/;
let result = lastRegex.test(caboose);

// \w is equal to [A-Za-z0-9_]
let quoteSample = "The five boxing wizards jump quickly.";
let alphabetRegexV2 = /\w/g;
let result = quoteSample.match(alphabetRegexV2).length;

// Match only 3 to 6 letter h's in the word "Oh no"
let ohStr = "Ohhh no";
let ohRegex = /Oh{3,6} no/;
let result = ohRegex.test(ohStr);

// Match both the American English (favorite) and the British English (favourite) version of the word
let favWord = "favorite";
let favRegex = /favou?rite/;
let result = favRegex.test(favWord);

// Groups () let you reuse patterns
let repeatNum = "42 42 42";
let reRegex =  /^(\d+)\s\1\s\1$/; // every 1 represent the group (\d+)
let result = reRegex.test(repeatNum);

// Remove all the spaces at the beginning an end of a string
let hello = "   Hello, World!  ";
let wsRegex = /^\s+(.*\S)\s+$/;
let result = hello.replace(wsRegex, '$1'); // returns 'Hello, World!'
```

---

## Bitwise Operators

### `&` (Bitwise AND)
Performs the `AND` operation on each pair of bits. The truth table for the AND operation is:

<table class="standard-table">
 <tbody>
  <tr>
   <td>a</td>
   <td>b</td>
   <td>a AND b</td>
  </tr>
  <tr>
   <td>0</td>
   <td>0</td>
   <td>0</td>
  </tr>
  <tr>
   <td>0</td>
   <td>1</td>
   <td>0</td>
  </tr>
  <tr>
   <td>1</td>
   <td>0</td>
   <td>0</td>
  </tr>
  <tr>
   <td>1</td>
   <td>1</td>
   <td>1</td>
  </tr>
 </tbody>
</table>

### `|` (Bitwise OR)
Performs the `OR` operation on each pair of bits. The truth table for the `OR` operation is:

<table>
 <tbody>
  <tr>
   <td>a</td>
   <td>b</td>
   <td>a OR b</td>
  </tr>
  <tr>
   <td>0</td>
   <td>0</td>
   <td>0</td>
  </tr>
  <tr>
   <td>0</td>
   <td>1</td>
   <td>1</td>
  </tr>
  <tr>
   <td>1</td>
   <td>0</td>
   <td>1</td>
  </tr>
  <tr>
   <td>1</td>
   <td>1</td>
   <td>1</td>
  </tr>
 </tbody>
</table>

### `^` (Bitwise XOR)
Performs the XOR operation on each pair of bits. The truth table for the XOR operation is:

<table>
<tbody>
  <tr>
   <td>a</td>
   <td>b</td>
   <td>a XOR b</td>
  </tr>
  <tr>
   <td>0</td>
   <td>0</td>
   <td>0</td>
  </tr>
  <tr>
   <td>0</td>
   <td>1</td>
   <td>1</td>
  </tr>
  <tr>
   <td>1</td>
   <td>0</td>
   <td>1</td>
  </tr>
  <tr>
   <td>1</td>
   <td>1</td>
   <td>0</td>
  </tr>
 </tbody>
</table>

### `~` (Bitwise NOT)
Performs the `NOT` operator on each bit. The truth table for the `NOT` operation is:

<table>
<tbody>
  <tr>
   <td>a</td>
   <td>NOT a</td>
  </tr>
  <tr>
   <td>0</td>
   <td>1</td>
  </tr>
  <tr>
   <td>1</td>
   <td>0</td>
  </tr>
 </tbody>
 </table>

---

## References

- [MDN Web Docs - JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [Modern JS Cheatsheet](https://github.com/mbeaudru/modern-js-cheatsheet)
- [Javascript Cheatsheet](https://github.com/wilfredinni/javascript-cheatsheet)
- [Airbnb Javascript](https://github.com/airbnb/javascript/blob/master/README.md)
- [Javascript Cheatsheet](https://websitesetup.org/javascript-cheat-sheet/)
