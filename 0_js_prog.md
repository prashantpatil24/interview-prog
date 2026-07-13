# JavaScript Interview Programs (Practice Collection)

# 1. Curry Function (Infinite Currying)

``` javascript
//normal curry function
function sum(a){
    return function(b){
        if(b === undefined){
            return a
        }
        return sum(a+b) 
    }
}
console.log(sum(1)())//1
console.log(sum(1)(2)())//3
console.log(sum(1)(2)(3)())//6
 
//using arrow_sum ==> es6
const arrow_sum = (a) => {
    return (b) =>{
       return  b === undefined ? a : arrow_sum(a+b)
    }
}
console.log(arrow_sum(1)())//1
console.log(arrow_sum(1)(2)())//3
console.log(arrow_sum(1)(2)(3)())//6
 
//using es6 arrow with shortcut
const arrow_short_sum = (a) => (b) => b === undefined ? a : arrow_short_sum(a+b)
console.log(arrow_short_sum(1)())//1
console.log(arrow_short_sum(1)(2)())//3
console.log(arrow_short_sum(1)(2)(3)())//6
```

# 2. Flatten Array

``` javascript
const biDimensionalArr = [11, [22, 33], [44, 55], [66, 77], 88, 99];

//default method
const flat = biDimensionalArr.flat(Infinity) 
console.log(flat) // [11,22,33,44,55,66,77,88,99]

//concat method
const concatFlat = [].concat(...biDimensionalArr)
console.log(concatFlat) // [11,22,33,44,55,66,77,88,99]

//by custom method
function myFlat(arr){
    return arr.reduce((acc,el)=> acc.concat(Array.isArray(el) ? myFlat(el) : ele) ,[])
}
console.log(myFlat(biDimensionalArr)) // [11,22,33,44,55,66,77,88,99]
```

# 3. Find Duplicate Characters in a String

``` javascript

function findDuplicates(str) {
    const map = {};
    const duplicate = [];

    for (let char of str) {
        map[char] = (map[char] || 0) + 1;

        if (map[char] === 2) {
            duplicate.push(char);
        }
    }

    return duplicate;
}

console.log(findDuplicates("programming")); // ['r','m','g']
```

# 4. Remove Duplicate Characters from a String

``` javascript

function removeDuplicatesByFlag(str) {
    const seen = {};
    const result = [];

    for (const char of str) {
        if (!seen[char]) {
            seen[char] = true;   // Assignment
            result.push(char);
        }
    }

    return result;
}

console.log(removeDuplicates("programming")); //[ 'p', 'r', 'o',   'g', 'a', 'm', 'i', 'n']
```

# 5. Find Unique (Non-Repeating) Characters

``` javascript

function uniqueCharacters(str) {
    const map = {};
    for (const ch of str) {
        map[ch] = (map[ch] || 0) + 1;
    }
    return Object.keys(map).filter(ch => map[ch] === 1);
}

console.log(uniqueCharacters("programming")); //['p', 'o', 'a', 'i', 'n']
```

# 6. Find Vowels in a String

``` javascript

function findVowels(str) {
    const vowels = ['a','e','i','o','u']
    const char = []
    for (const ch of str) {
        if(vowels.includes(ch)){
            char.push(ch)
        }
    }
    return char;
}
console.log(findVowels("programming")); 
```

# 7. Promise Retry with Timeout Mechanism

``` javascript

async function retry(fn, retries = 3, delay = 1000) {
    for (let attempt = 1; attempt <= retries; attempt++) {
        try {
            return await fn();
        } catch (err) {
            console.log(`Attempt ${attempt} failed`);

            if (attempt === retries) {
                throw err;
            }

            await new Promise(resolve => setTimeout(resolve, delay));
        }
    }
}

let count = 0;

async function fetchData() {
    count++;
    console.log("Calling API:", count);

    if (count < 4) {
        throw new Error("Request failed");
    }

    return {
        id: 1,
        name: "Test"
    };
}

retry(fetchData, 4, 2000)
    .then(console.log)
    .catch(console.error);
```

# 8. Count Element Frequency in an Array

``` javascript

function countElementInArray(arr){
    let count = {}
    arr.forEach((item)=> count[item] = (count[item]||0) + 1)
    return count
}

function countElementInArrayByReduceMethod(arr){
    return arr.reduce((acc,item)=> {
         acc[item] = (acc[item]||0) + 1 
        return acc
    },{})
}
console.log(countElement([1,2,3,1,2,3,4,5,7,1,2,4]))
console.log(countByReduce([1,2,3,1,2,3,4,5,7,1,2,4]))
//{ '1': 3, '2': 3, '3': 2, '4': 2, '5': 1, '7': 1 }
```

# 9. Find First Non-Repeated Character

``` javascript

function findFirstNotRepeatedChar(str) {
    const count = {};

    // Count frequency
    for (const char of str) {
        count[char] = (count[char] || 0) + 1;
    }

    // Find first non-repeated character
    for (const char of str) {
        if (count[char] === 1) {
            return char;
        }
    }

    return null; // No unique character found
}

console.log(findFirstNotRepeatedChar("abcdefabcdefgh")); // g
```

# 10. Debounced Search in JavaScript

``` javascript

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Debounce Search</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
        }

        input {
            width: 300px;
            padding: 10px;
            font-size: 16px;
        }

        #debounce {
            display: block;
            margin-bottom: 15px;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div id="root">
    <span id="debounce"></span>
    <input
        type="text"
        id="search"
        placeholder="Search..."
    />
</div>

<script>

    const searchField = document.getElementById("search");
    const debounceField = document.getElementById("debounce");

    function debounce(fn, delay) {
        let timer;
        return function (...args) {
            clearTimeout(timer);
            timer = setTimeout(() => {
                fn(...args);
            }, delay);
        };
    }

    function handleApiCall(e) {
        const value = e.target.value.trim();
        if (!value) {
            debounceField.textContent = "";
            return;
        }
        debounceField.textContent = value;
        console.log("API Call:", value);
    }

    const handleSearch = debounce(handleApiCall, 1000);
    searchField.addEventListener("input", handleSearch);

</script>

</body>
</html>
```

# 11. Deep Copy in JavaScript

``` javascript

    // Original Array
    const a = [
        { id: 1, name: "test_1" },
        { id: 2, name: "test_2" }
    ];

    // -------------------------
    // 1. Deep Copy using JSON
    // -------------------------

    const b = JSON.parse(JSON.stringify(a));

    b[0].name = "test_3";

    console.log("Original:", a);
    console.log("JSON Copy:", b);

    // -------------------------
    // 2. Deep Copy using structuredClone()
    // -------------------------

    const c = structuredClone(a);

    c[0].name = "test_4";

    console.log("Original:", a);
    console.log("structuredClone:", c);

    // -------------------------
    // 3. Deep Copy using Recursion
    // -------------------------

    function deepCopy(obj) {

        if (typeof obj !== "object" || obj === null) {
            return obj;
        }

        const copy = Array.isArray(obj) ? [] : {};

        for (const key in obj) {
            copy[key] = deepCopy(obj[key]);
        }

        return copy;
    }

    const d = deepCopy(a);

    d[0].name = "test_5";

    console.log("Original:", a);
    console.log("Recursive Copy:", d);
```
# 11. Memoization

``` javascript

function memo() {
    const cache = {};

    return function (val) {
        if (val in cache) {
            console.log("Cache Hit");
            return cache[val];
        }

        console.log("Calculating...");

        const result = val + 10;

        cache[val] = result;

        return result;
    };
}

const calculate = memo();

console.log(calculate(10));  
//Calculating...
//20
console.log(calculate(10));
//Cache Hit
//20
console.log(calculate(20));
//Calculating...
//30
console.log(calculate(30));
//Calculating...
//40
console.log(calculate(10));
//Cache Hit
//20

```
# 12. Anagram

``` javascript
  
  //default method
  function isAnagram(source, target){
    return source.split("").sort().join("") === target.split("").sort().join("")
  }
  console.log(isAnagram('listen','silent'))

  //by custom function
  function isAnagramByCustom(source, target){
    const count = 0
    for(let char of source){
      map[char] = (map[char] || 0) + 1
    }
    for(let char of target){
      if(!count[char]) return false
      count[char]--
    }
    return true
  }
  console.log(isAnagramByCustom('listen','silent'))
```

# 13. Bracket Matcher

```javascript

function bracketMatcher(str) {
  const stack = [];

  for (let i of str) {
    if (i == '(' || i == '[' || i == '{') {
      stack.push(i);
    } else if (i == ')' || i == ']' || i == '}') {
      if (stack.length === 0) {
        return false;
      }
      let top = stack.pop();
      if (
        (i == '(' && top != ')') ||
        (i == '{' && top != '}') ||
        (i == '[' && top != ']')
      ) {
        return false;
      }
    }
  }
  return stack.length === 0 ? true : false;
}
console.log(bracketMatcher('(coder)(byte)')); // true
console.log(bracketMatcher('{[(])}')); // false
console.log(bracketMatcher('((()))')); // true
console.log(bracketMatcher('(()')); // false

```
# 14. Sum of equal target

```javascript

//Input const arr = [2,3,8,7,6]
// target  9
// output [0,3]

function findSumOfEqualTarget(arr, target){
   const map = new Map()

   for(let i=0; i< arr.length; i++){
      const sub = target - arr[i] 
      if(map.has(sub)){
        return [map.get(sub),i]
      }
      map.set(arr[i], i)
   }
   return [] 
}
/*
sub 7 => map Map(0) {}
sub 6 => map Map(1) { 2 => 0 }
sub 1 => map Map(2) { 2 => 0, 3 => 1 }
sub 2 => map Map(3) { 2 => 0, 3 => 1, 8 => 2 }
[ 0, 3 ]
*/
console.log(findSumOfEqualTarget([2,3,8,7,6],9))//[0,3]

```
# 14. Find the largest number with the second-highest frequency.

```javascript

//Input [1,2,2,2,3,3,3,4,4,5,5]
//Output  5

function findSecondLargest(arr) {
    const freq = {};

    for (const num of arr) {
        freq[num] = (freq[num] || 0) + 1;
    }

    const frequencies = [
        ...new Set(Object.values(freq))
    ].sort((a, b) => b - a);

    if (frequencies.length < 2) {
        return -1;
    }

    const secondHighest = frequencies[1];

    const candidates = Object.keys(freq)
        .filter(key => freq[key] === secondHighest)
        .map(Number);

    return Math.max(...candidates);
}

console.log(findSecondLargest([1,2,2,2,3,3,3,4,4,5,5])); // 5
```
# 15. Custom Map

```javascript

Array.prototype.myMap = function (cb){
  const result = []
  for(let i=0; i< this.length; i++){
    result.push(cb(this[i],i,this))
  }
  return result
}
const result = [1,2,3].myMap(item => item*2)
console.log(result) //[ 2, 4, 6 ]

```
# 16. Custom Filter

```javascript

Array.prototype.myFilter = function (cb){
  const result = []
  for(let i=0; i< this.length;i++){
    if(cb(this[i], i, this)){
      result.push(this[i])
    }
  }
  return result
}
const result = [1,2,3,4].myFilter(item => item%2 == 0)
console.log(result) //[ 2, 4]

```
# 17. Custom Reducer

```javascript

Array.prototype.myReducer = function(callback, initialValue) {
   let accumulator = initialValue;
   let startIndex = 0;
   
   // Handle no initial value
   if (accumulator === undefined) {
       accumulator = this[0];
       startIndex = 1;
   }
   for (let i = startIndex; i < this.length; i++) {
       accumulator = callback(accumulator, this[i], i, this);
   }
   return accumulator;
};

const result = [1,2,3,4].myReducer((acc,item)=> acc = acc + item ,0)
console.log(result) //10

```

# 18. Flat nested array 

```javascript

//default method 
const flatArray = [1,2,3,[4,5,6],[5,6]].flat(Infinity)
console.log(flatArray)

//custom method
function flatten(arr){
 return arr.reduce((acc,item)=>{
   return acc.concat(Array.isArray(item) ? flatten(item) : item)
 },[])
}

console.log(flatten([1,2,3,[4,5,6],[5,6]]))
```
# 19. Group By key

```javascript

const users = [
 { name: "A", age: 20 },
 { name: "B", age: 20 },
 { name: "C", age: 30 }
];

function groupByKey(arr){
    const map = {}

    for(let [key,value] of arr.entries()){
      const {name, age} = value
      if(!map[age]){
          map[age] = []
      }
      map[age].push(value)
    }
    return map
}
console.log(groupByKey(users))

//by reduce method
function groupByReduce(arr){
  return arr.reduce((acc,ele) =>{
     const value = ele.age
     if(!acc[value]){
      acc[value] = []
     }
     acc[value].push(ele)
     return acc
  }, {})
}
console.log(groupByReduce(users))
//output
/*{
  '20': [ { name: 'A', age: 20 }, { name: 'B', age: 20 } ],
  '30': [ { name: 'C', age: 30 } ]
}
*/

```
# 20. Find missing num

```javascript
function findMissingNum(arr){
   const totalElement = arr.length + 1 
   const result = (totalElement *(totalElement + 1)) / 2    // (5*6) / 2 = 15
   const sum = arr.reduce((acc,item)=> acc = acc + item ,0) // 11
   return result - sum //15-11 = 4
}
console.log(findMissingNum([1,2,3,5])) //4

```

# 20. Repeat String

```javascript

function getRepeatString(arr){
   const result = []
   for(let i=0; i <arr.length;i++){
     const [char,num] = arr[i].split('')
     result.push(char.repeat(num)) 
   }
   return result
}
console.log(getRepeatString(['a2','b3','c4'])) //['aa','bbb','cccc']

function getRepeatStringWithReduce(arr){
   return arr.reduce((acc,item)=>{
       const [char,num] = item
       acc.push(char.repeat(num))
       return acc
   } ,[])
}
console.log(getRepeatStringWithReduce(['a2','b3','c4'])) //['aa','bbb','cccc']

```
# 21. Reverse array

```javascript

const arr = [1,2,3,4,5]

//slice method
console.log(arr.slice().reverse())

//spread method
console.log([...arr].reverse())

//reduce
const c = arr.reduce((acc, item)=> [item, ...acc], [])
console.log(c)

//default method
console.log(arr.sort((a,b) => b-a)) //modified array

```





