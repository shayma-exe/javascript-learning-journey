# 📓 Lesson 12: Advanced Functions

---

## 🗺️ Table of Contents
To help you navigate through this note 👇

1. [Hoisting](#1-hoisting)
2. [callBack](#2-callback)
3. [forEach()](#3-foreach)
4. [setTimeout()](#4-settimeout)
5. [setInterval()](#5-setinterval)
6. [Exercises](#6-exercises)

---

## 1. Hoisting

### 🧠 The Core Concept
We can call the function (its name) before its body code

### 💻 Example :
```JavaScript
greeting()
function greeting() {
  console.log('hello');
}
```
👀 Notice how we invoke `greeting()` before its body (function declaration) later on  
**How can that be possible :O ?**  
The JavaScript engine *scans* our file and allocates memory for function declarations **BEFORE** executing the code line-by-line

---

## 2. callBack

### 🧠 The Core Concept
Passing a function into another one !  
**How is that possible ?**  
Paramaters takes values, right ?    
Function are just another type of values : `valueOf(function(){...})` returns 'function'  

### 💻 Example Syntax :
Let's build one together :D !   
1. First the 'mother' function = receiving into it's params  
👀 Notice how we treated `param` just like a function inside `run()`'s body

```JavaScript
function run(param) {
  param();
}
```
2. We'll call this `run(...)` function  below  
**The new thing ?**   
We're passing **another** function as a parameter inside it !  
```JavaScript
run(function() {
  console.log('hello');
})
```


---
## 3. forEach()

### 🧠 Core Concept
Array's 'for' loop alternative   
A method from the *array* class = call it from an array object :)  
Takes 2 params `function(value,index)`    
**1st :**  value of a specific element in the array  
**2nd :** index of that same element    
/!\ Params order is important.  

### 💻 Example Syntax :
```javascript
[
  'make dinner',
  'wash dishes',
  'watch youtube'
].forEach(function(value, index) {
  console.log(index);
  console.log(value);
})
```
👀 Notice how we created an array first, then called .forEach() method from it

---
## 4. setTimeout()

### 🧠 Core Concept
Run a function in the future
How it works ?     
Set a timer, but **doesn't** wait for it to finish and keep running the code below  
This has a name : Asynchronous Code !  
- **Asynchronous code** = immediatly goes to the next line with the other code still running in the background
- **Synchronous code** = Runs code line by line



---

## 5. setInterval()

### 🧠 Core Concept
Keep running a function after a certain amount of time

---

## 6. Exercises
Some exercises I solved using the concepts seen above along with my notes and reflections on each  
enjoy the trip ;) 

### 1. 'ADDED' button 

```HTML
<script>
      let timeoutId;

      function displayMessage() {
        const messageElement = document.querySelector('.js-message');
        messageElement.innerHTML = 'Added';

        // First, cancel the previous timeout so that
        // it doesn't remove the message too quickly.
        clearTimeout(timeoutId);

        timeoutId = setTimeout(function() {
          messageElement.innerHTML = '';
        }, 2000);
      }
    </script>
```

**⛔ Problem We had**  
Clicking the button 2 times before the first 2sec ends : it didn't refreshed the timer, and it still ended in 2s  
Why ?  
When clicking a second time, yes a second setTimeout start running, until the timer of the first ends it = messages dispears  

**Solution !**
- Before running `setTimeout()` again : clear the first timer `clearTimeout(timeoutId);` = prevents it from endding its timer and therefore making the message disapear
- Save returned ID into a variable `timeoutId = setTimeout(...` in case the button is clicked again, we can clear its timer !





