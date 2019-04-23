## Find longest palindrome in a given string
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
//Output: ["acdg", "bcdg", "aceg", "bceg", "acfg", "bcfg", "acdh", "bcdh", "aceh", "bceh", "acfh", "bcfh", "acdi", "bcdi", "acei", "bcei", "acfi", "bcfi"]

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
Ans: A custom element extends HTML by allowing you to define a tag whose content is created and controlled by JavaScript code.
The browser maintains a CustomElementRegistry of defined custom elements (also called Web Components), which maps an instantiable JavaScript class to an HTML tag.

The @angular/elements package exports a createCustomElement() API that provides a bridge from Angular component interface and change detection functionality to the built-in DOM API.

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
