
## Count how many times button is clicked without using global variable
```javascript
var my_button = document.getElementById('myButton');
myButton.addEventListener('click', function(){
	++document.getElementById('counter').innerHTML;
});

<input type="button" id="myButton" value="Click"/>
Counter: <label id="counter"></label>
```

## How to make array empty and which is best way
```javascript
// We can make an array empty in different ways , below are some of them

// method 1
let mainArray = ["1","2","3"]
mainArray=[];
console.log(mainArray); // []

//Method 2
let secondArray = ["1","2","3"]
secondArray.length=0
console.log(secondArray); // [] 

//1st way we are creating another empty array but in second array we are 
//making existing array length 0.
```
## Date format in javascript
```javascript
// Write a function that converts user entered date formatted as M/D/YYYY to a format required by an 
// API (YYYYMMDD). The parameter "userDate" and the return value are strings.
// For example, it should convert user entered date "12/31/2014" to "20141231" suitable for the API.
   function formatDate(userDate) {
     // format from M/D/YYYY to YYYYMMDD
     return new Date(userDate).yyyymmdd();
   }

   Date.prototype.yyyymmdd = function() {
       var yyyy = this.getFullYear().toString();                                    
       var mm = (this.getMonth()+1).toString(); // getMonth() is zero-based         
       var dd  = this.getDate().toString();
       return yyyy + '' + (mm[1]?mm:"0"+mm[0]) + '' + (dd[1]?dd:"0"+dd[0]);
   };

   console.log(formatDate("12/31/2014"));

// Output: 20141231
```

## Ensure function
```javascript
// ensure function so that it throws an error if called without arguments or the argument is undefined.
// Otherwise it should return the given value.
   function ensure(value) {
      if (value == undefined) {
         throw new Error('no arguments');
      } else {
      return value;
      }   
   }
```


## Ways to create JS objects

```javascript

// Using the Object() constructor:
   var d = new Object();
   // This is the simplest way to create an empty object. I believe it is now discouraged.

// Using Object.create() method:
   var a = Object.create(null);
   // This method creates a new object extending the prototype object passed as a parameter.

// Using the bracket's syntactig sugar:
   var b = {};
   This is equivalent to Object.create(null) method, using a null prototype as an argument.

// Using a function constructor
   var Obj = function(name) {
   this.name = name
   }
   var c = new Obj("hello"); 
   // What the new operator does is call a function and setting this of the function to a fresh new Object, 
   // and binding the prototype of that new Object to the function's prototype. As is:

   function f {};
   new f(a, b, c);
   
   // Would be equivalent to: 
   
   // Create a new instance using f's prototype.
      var newInstance = Object.create(f.prototype)
      var result;
   
      // Call the function
      result = f.call(newInstance, a, b, c),
      // If the result is a non-null object, use it, otherwise use the new instance.
      result && typeof result === 'object' ? result : newInstance

// Using the function constructor + prototype:
   function myObj(){};
   myObj.prototype.name = "hello";
   var k = new myObj();

// Using ES6 class syntax:
   class myObject  {
      constructor(name) {
      this.name = name;
      }
    }
    var e = new myObject("hello");
    
// Singleton pattern:
   var l = new function() {
       this.name = "hello";
   }
```

## Ways to create JS objects 
// is it exactly the same as:
```javascript
var p = {} vs var p2 = Object.create(null) ?

// They are not equivalent. {}.constructor.prototype == Object.prototype while Object.create(null) doesn't inherit 
// from anything and thus has no properties at all.
// In other words: A javascript object inherits from Object by default, unless you explicitly create it with null 
// as its prototype, like: Object.create(null).

// {} would instead be equivalent to Object.create(Object.prototype).

In Chrome Devtool you can see that Object.create(null) has no __proto__ property, while {} does.
![object create ](https://cdn-images-1.medium.com/max/800/1*rSHmnlUotrjc5lXV1xDtGA.png)

// ref: https://hackernoon.com/object-create-in-javascript-fa8674df6ed2

```


## Promise and Callback

Promise: The Promise object represents the eventual completion (or failure) of an asynchronous operation, 
         and its resulting value.
// Example: 
```javascript
 var promise1 = new Promise(function(resolve, reject) {
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
 A Promise is in one of these states:
 pending: initial state, neither fulfilled nor rejected.
 fulfilled: meaning that the operation completed successfully.
 rejected: meaning that the operation failed.
 
 A pending promise can either be fulfilled with a value, or rejected with a reason (error). 
 When either of these options happens, the  associated handlers queued up by a promise's then 
 method are called. (If the promise has already been fulfilled or rejected when a corresponding 
 handler is attached, the handler will be called, so there is no race condition between an asynchronous 
 operation completing and its handlers being attached.)
 
 As the Promise.prototype.then() and Promise.prototype.catch() methods return promises, they can be chained.
 ![promise structure](https://mdn.mozillademos.org/files/15911/promises.png)
 
Callback function : A callback function is a function passed into another function as an argument, which is 
                    then invoked inside the outer function to complete some kind of routine or action.

```javascript
// Example:
 function greeting(name) {
  alert('Hello ' + name);
 }

 function processUserInput(callback) {
  var name = prompt('Please enter your name.');
  callback(name);
 }
 processUserInput(greeting);
 // The above example is a synchronous callback, as it is executed immediately.
 Note, however, that callbacks are often used to continue code execution after an asynchronous operation 
 has completed — these are called asynchronous callbacks. A good example is the callback functions executed 
 inside a .then() block chained onto the end of a promise after that promise fulfills or rejects. This 
 structure is used in many modern web APIs, such as fetch().
```


## Get the closest next or previous integer in a sorted array of integers
```javascript
// array = sorted array of integers
// val = pivot element
// dir = boolean, if true, returns the previous value
 
function getVal(array, val, dir) {
  for (var i=0; i < array.length; i++) {
    if (dir == true) {
      if (array[i] > val){
        return array[i-1] || 0;
      }
    } else {
      if (array[i] >= val) {
        return array[i];
      }
    }
  }
}

var array = [0, 5, 7, 9, 22, 27];
var pivot = 11;
 
getVal(array, pivot);        //Output: 22
getVal(array, pivot, true);  //Output: 9

```

## Function Expression VS. Function Statement
```javascript
// Example: Function Expression
    alert(foo()); // ERROR! foo wasn't loaded yet
    var foo = function() { return 5; }
    
// Example: Function Declaration
    alert(foo()); // Alerts 5. Declarations are loaded before any code can run.
    function foo() { return 5; }
    
// Function declarations load before any code is executed while Function expressions load only when the 
interpreter reaches that line of code.
    
// Benefits of Function Expressions
There are several different ways that function expressions become more useful than function declarations.    
  1. As closures
  2. As arguments to other functions
  3. As Immediately Invoked Function Expressions (IIFE)
```

## Find the Max & Min number from given array in javascript
```javascript
    let arr = [1, 4, 6, 2, 9, 5, 3, 10];
    console.log("find largest number : " + Math.max.apply(null, arr));
    //Output: 10
    console.log("find smallest number : " + Math.min.apply(null, arr));
    //Output: 1
```

## Find longest palindrome in a given string in javascript
```javascript
console.log(longest_palindrome("HYTBCABADEFGHABCDEDCBAGHTFYW12345678987654321ZWETYGDE"));
//Output: 12345678987654321

function longest_palindrome(str1) {
    var max_length = 0,
        maxp = '';

    for (var i = 0; i < str1.length; i++) {
        var subs = str1.substr(i, str1.length);

        for (var j = subs.length; j >= 0; j--) {
            var sub_subs_str = subs.substr(0, j);
            if (sub_subs_str.length <= 1)
                continue;

            if (isPalindrom(sub_subs_str)) {
                if (sub_subs_str.length > max_length) {
                    max_length = sub_subs_str.length;
                    maxp = sub_subs_str;
                }
            }
        }
    }

    return maxp;
}
```

## How to Get all Possible Combinations of Array with array length  
```javascript
console.log(posibleCombinationsOfArr([['a', 'b'], ['c'], ['d', 'e', 'f'], ['g', 'h', 'i']]));
//Output: ["acdg", "bcdg", "aceg", "bceg", "acfg", "bcfg", "acdh", "bcdh", "aceh", "bceh", "acfh", "bcfh", "acdi", 
// "bcdi", "acei", "bcei", "acfi", "bcfi"]

function posibleCombinationsOfArr(combinationArr) {
  if (combinationArr.length === 1) {
    return combinationArr[0];
  } else {
    var result = [];
    if (combinationArr.length > 1) {
      var allCasesRest = posibleCombinationsOfArr(combinationArr.slice(1));
      for (var i = 0; i < allCasesRest.length; i++) {
        for (var j = 0; j < combinationArr[0].length; j++) {
          result.push(combinationArr[0][j] + allCasesRest[i]);
        }
      }
      return result;
    }
  }
}
```
## How to Extend String Methods as default method
```javascript
console.log("abcd".repeat(3));
// Output: repeated string is abcdabcdabcd

String.prototype.repeat = function repeat(num) {
  var str = '';
  for (var i = 0; i < num; i++) {
    str += this;
  }
  return str;
}
```

## Get All combinations of a given String
```javascript
console.log("all Combinations" + getAllCombinations(abcd));
// Output: all Combinations=abcd,abc,abd,ab,acd,ac,ad,a,bcd,bc,bd,b,cd,c,d,

const abcd = "abcd";
function getAllCombinations(abcd) {
  const fn = function (active, rest, arr) {
    if (!rest) {
      arr.push(active);
    } else {
      fn(active + rest[0], rest.slice(1), arr);
      fn(active, rest.slice(1), arr);
    }
    return arr;
  }
  return fn('', abcd, []);
}
```

## How to reverse a given string
```javascript
console.log( reverseSTR('Hello') );
// Output: olleH

function reverseSTR(str) {
  let res = '';
  for (let i = str.length - 1; i >= 0; i--) {
    res += str[i];
  }
  return res;
}
```
## Example on async and await
```javascript
async function await() {
  let promise = new Promise((resolve, reject) => {
    setTimeout((x) => {
      return resolve(x);
    }, 3000, 'got it');
  });
  let result = await promise;
  alert(result);
}
await().then( (data) => {
  alert("Some operation/action");
});
```
## curry sum function with unordered parameters 
```javascript
console.log("do sum=" + dosum(2, 5)(3)());
// Output: do sum=10
console.log(add(2)(3)());
// 5

function dosum(...args) {
  let s = args.reduce((a, b) => a + b);
  return function (...x) {
    return x.length == 0 ? s : dosum(s, ...x);
  }
}

function add(x) {
  return function sum(y) {
    if (y === undefined) {
      return x;
    } else {
      x = x + y;
      return sum;
    }
  }
}
```

## Get arguments length
```javascript
console.log( argLen(2, 3, 4, 5, 7) );
// Output: 5

let ds = function () {
  return [].slice.call(arguments).length;
}
```

## Simplest or Cleanest way to implement singleton in JavaScript
```javascript
// Singleton is an object which can only be instantiated once. 
// it is a pattern which creates a new instance of the class if one doesn't exist, if an 
// instance already exists, it returns the reference to that object.
var Singleton = (function () {
    var instance;
 
    function createInstance() {
        var object = new Object("I am the instance");
        return object;
    }
 
    return {
        getInstance: function () {
            if (!instance) {
                instance = createInstance();
            }
            return instance;
        }
    };
})();
 
function run() {
 
    var instance1 = Singleton.getInstance();
    var instance2 = Singleton.getInstance();
 
    alert("Same instance? " + (instance1 === instance2));  
}
```

## Object comparision
```javascript
var person = {name: 'person'};
objComparision(person);

function objComparision(obj) {
  if ( obj === {name: 'person'} ) {
    console.log('Object Comparison Sucess');
  } else {
    console.log('Object Comparison Fail');
  }
}

// Output: Object Comparison Fail
// Description: Objects are typeless and reference allocated in memory differs
```

## Console log returns True or False
```javascript
console.log("returns true or false start");
console.log([]); //empty array
console.log({}); //empty object
console.log(typeof [] + []); // object
console.log({} + []); // [object Object]
console.log(1); // 1
console.log(0); // 0
console.log(100); // 100
console.log("false" + false); // falsefalse
console.log("true" + true); // truetrue
console.log("false"); // false
console.log("true"); // true
console.log(false); // false
console.log(true); // true
console.log(false + true); // 1
console.log(true + false); // 1
console.log(true + true); // 2
console.log(false + false); // 0
console.log("returns true or false end");
```

## Bubble sort given array and convert result to string
```javascript
function bubbleSort(arr) {
  for (var i = 0; i < arr.length; i++) {
    for (var j = 0; j < arr.length - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        var a = arr[j];
        var b = arr[j + 1];
        arr[j] = b;
        arr[j + 1] = a;
      }
    }
  }
  return arr;
}
console.log(bubbleSort(array)); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
console.log("sort = " + array.sort()); // sort = 1,2,3,4,5,6,7,8,9
```

## Commonly asked Javascript and Angular Questions
```javascript
### 1. How to communicate between two unrelated components ?
Ans: using subjects, event emiters, getters and setters or service

### 2. What are angular elements and example ?
Ans: A custom element extends HTML by allowing you to define a tag whose content is created and controlled by 
JavaScript code. The browser maintains a CustomElementRegistry of defined custom elements (also called Web Components), 
which maps an instantiable JavaScript class to an HTML tag.

The @angular/elements package exports a createCustomElement() API that provides a bridge from Angular component 
interface and change detection functionality to the built-in DOM API.

import { BrowserModule } from '@angular/platform-browser';
import { NgModule, Injector } from '@angular/core';
import { createCustomElement } from '@angular/elements';
 
import { HelloComponent } from './hello.component';
 
@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  providers: [],
  entryComponents: [HelloComponent]
})
export class AppModule {
  constructor(injector: Injector) {
    const el = createCustomElement(HelloComponent, { injector });
    customElements.define('nrwl-hello', el);
  }
 
  ngDoBootstrap() {}
}

As you can see, we added our component to the entryComponents array and then use createCustomElement function to create the 
element out of it. You’ll also note that we did not include the bootstrap array within our NgModule configuration, and we 
overrode the ngDoBootstrap lifecycle hook with an empty method.

Once we have the custom element, we add it to the custom elements registry by using the define method. We can then include 
the app on the page and instantiate the element by adding this to the DOM:

<nrwl-hello></nrwl-hello>
The browser will see the element and will instantiate the Angular component.

### Why Angular Elements?
There are five main reasons to use Angular elements.

Reason 1: Embedding Angular Components Into Non-Angular Applications
All framework speak “custom elements”, at least to some degree. So if you want to embed an Angular component into your React, 
Vue, or Ember app, just wrap it into a custom element. Having said that, we at Nrwl recommend you to avoid mixing frameworks 
unless you have a very good reason to.

Reason 2: Embedding Angular Components Into Content Sites
If you have a server-side (e.g. ASP.net) application you want to sprinkle with some Angular magic, Angular Elements are the 
easiest way to do it.

Reason 3: Implementing Dynamic Angular Applications (“Dashboard”/CMS)
Seemingly every other application we look at contains a requirement for some kind of dynamic dashboard. Usually such a 
dashboard has to be assembled from a fixed set of Angular components using some metadata. This has to happen at runtime, so we 
cannot precompile an assembled dashboard.

If your requirements allow you to configure the dashboard using JSON, you could write an interpreter component that will assemble 
the dashboard at runtime using DynamicComponentLoader.

This, however, doesn’t work for more advanced scenarios. If you have a CMS allowing agents to author custom HTML containing 
Angular elements, the above approach will break down. In AngularJS we could use $compile for that, with Angular elements, we 
can use the browser itself by simply injecting some HTML:


Reason 4: Upgrading from AngularJS to Angular
Using the @angular/upgrade package you can mix and match AngularJS and Angular components and services, but that’s only one
of the challenges we face when upgrading apps.

Say you bundle your AngularJS app using RequireJS and your angular code using Webpack? The resulting formats are different,
the lazy loading mechanisms are different. How do you marry the two? How do you make sure there are no race conditions when 
lazy loading code? What about zone.js? It’s hard.

An upgrade strategy built around Angular elements doesn’t suffer from any of these issues. You could bundle Angular Elements
into UMD bundles and load them using RequireJS.

In our experience, using elements is a viable approach that works well for the situations where the complexity of mixing and 
matching components is overshadowed by the complexity of marrying the two tech stacks.

Many teams at Google are also using this approach to upgrade their AngularJS apps. The Angular team has privately endorsed 
upgrading as a valid use case for Angular Elements.

Reason 5: Independent Deployment
If your organization wants to develop and publish parts of an application independently, elements are a great way to achieve 
that.

### 3. How to create custom decorators ? 
Ans: 


### 4. what is the input for AOT compilation process ?
Ans: .d.tf files are inputs. The TypeScript compiler does some of the analytic work of the first phase. It emits the .d.ts type definition files with type information that the AOT compiler needs to generate application code.
At the same time, the AOT collector analyzes the metadata recorded in the Angular decorators and outputs metadata information
in .metadata.json files, one per .d.ts file.

### 5. Diff between Map, Weakmaps, Set, weaksets
Ans: Jaascript Data Types are object and array, In object and array we cannot set key as different data types.
example : var x = { { y: 5} : 3 }
newly introduced maps and sets, we can able to do.

### 6. Javascript Closure example, what is the below code out put and fix ?
for (var i = 0; i < 4; i++) {
  setTimeout(function () {
    console.log(i);      
  }, 3000);  
}
// Output: 4 4 4 4 

#### 1. fix for below code
for (var i = 0; i < 10; i++) {
  (function (x) {
    setTimeout(function () {
      // console.log(x);      
    }, 3000);
  })(i);
}
#### 2. fix for below code
for (var i = 0; i < 10; i++) {
  setTimeout(function (x) {
    console.log(x);      
  }, 3000, i);
}
// Output: 1234

### 7. Diff between promise and Observables

### 8. what are Singleton and factories in jvascript

### 9. How can you say your code is a Good Code ?
Ans: following design patterns, also describe each of them

### 10. Scrum meeting disadvantages ?

### 11. Javascript Eventloop ?

### 12. what is GitFlow ? 

### 13. Javascript Event Delegation ? 

### 14. 
```
