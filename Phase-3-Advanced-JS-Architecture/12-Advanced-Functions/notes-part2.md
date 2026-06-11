# 📓 Lesson 12: Advanced Functions (part2)

---

## 🗺️ Table of Contents
To help you navigate through this note 👇

1. [Shorter Syntax: Arrow Functions](#1-shorter-syntax-arrow-functions)
2. [addEventListener]
3. [Filter]
4. [Map]

---

## 1. Shorter Syntax: Arrow Functions
### 🧠 The Core Concept
Arrow functions provide a clean shortcut to write regular functions.  
We'll see down when to use each.  

### 💻 Syntax
```JavaScript
const arrowFun = (params) => {
  //Your code here
}
```

**Wants more shortcuts ?**
- Single parameter ? Drop parentheses `(...)` ❌  
`const oneParam = event => {...} `
- One line of code ? Drop `{...}` and `return` keyword ❌ 
- `const oneLine = event => 2 + 3 `

### ⚖️ Regular function VS arrow function : what to choose ?
- **Use arrow function for callBacks :** Perfect when passed as arguements inside the params of another function (like `forEach()`)
- **Choose regular function for structural framework :** Hoisting (invoking a function before it's definition) & inside objects

✋🏻 Wait, want an example about calling a function inside an object ?  
We call that : shorthand   

**❌ Bad Practice : arrow function**  
```JavaScript
const object = {
  method: () => {
  // Cannot safely access "this" properties
  }
}
```

**👍🏻 Good Practice : shorthand**  
```JavaScript
const object = {
  method() {
  // Perfectly scoped execution block :D
  }
}
```
