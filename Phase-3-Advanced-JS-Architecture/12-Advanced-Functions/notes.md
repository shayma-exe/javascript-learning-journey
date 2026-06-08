# 📓 Lesson 12: Advanced Functions

---

## 🗺️ Table of Contents
To help you navigate through this note ;)
1. [Hoisting](#1-hoisting)
2. [callBack](#2-callback)
3. [Array's 'for' loop alternative : forEach()](#3-foreach)
4. [Run funtion when timer ends : setTimeout()](#4-settimeout)
5. [Run function multiple time : setInterval()](#5-setinterval)

---

## 1. Hoisting

---

## 2. callBack

### 🧠 The Core Concept
Passing a function into another one !  
**How is that possible ?**  
Paramaters takes values, right ?    
Function are just another type of values : `valueOf(function(){...})` returns 'function'  

### 💻 Example Syntax :
Let's build one together :D !   
1. First the 'mother' function = receiving

```JavaScript
function run(param) {
  param();
}
```
2. We'll call this same function `run(...)` below  
**The new thing ?**   
We're passing **another** function inside it !  
```JavaScript
run(function() {
  console.log('hello');
})
```


---
## 3. forEach()

### 🧠 The Core Concept
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
Result : 
Notice here how we created an array first, then called .forEach() method from it

---
## 4. setTimeout()

---

## 5. setInterval()



