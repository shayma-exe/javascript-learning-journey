# 🧪 Web Application Testing with Jasmine
In this lesson, we'll learn how to use a framework to test the code of our project, implementing 'Unit' and 'Integration' tests.  
At the end you'll be able to understand those 'words', how a test work.  

---
## 📋 Table of Contents

---

## 🧠 Testing Fundamental Concepts

### Manual vs. Automated Testing :
**- Manual Testing :** Simply open the website and try it out.  
**Cons ?** 👉🏻 Hard to test EVERY situation.  
*Exemple :* different currency : 20.00 $ or 0.00 $  
"Maybe it works for the current variable the page's displaying, but you have no garantee once the variable changes.."  

**- Automated testing :** Using code to test code.   
We explicitly tell the computer to do these tests for us !

### How many test cases should we have :
- **Basic Cases :** Verifying expected behavior "Is the code working ?"
- **Edge cases :** Testing risky values "Can this same code do X ?" 

---
## 🛠️ Testing before frameworks 

Here's the pratical steps :  
1. Create a dedicated test file for each file we wanna test from our project.
2. At the top of the brand new file, import the functions to test.
3. Using 'if-statement' write expected result for every different scenario.
4. Create ONE HTML file to load ALL these tests using `<script>` tags.

Inside a test file, what's the architecture ?  
1. Create test suite `console.log('test suite : ...')`.
2. Create tests inside the suite `console.log('test name ...')`
3. Compare values and display result (passed/failed) `ìf(...){//Passed/failed}`

💻 Syntax example :
```JavaScript
import {formatCurrency} from "../scripts/utils/money.js";

console.log('Test suite : formatCurrency');

console.log('convert cents into dollars');

if (formatCurrency(2095) === '20.95') {
  console.log('passed');
} else {
  console.log('failed');
}

```
---
## 🛠️ Jasmine Setup & Directory Architecture

#### What's Jasmine ?
A testing framework that let us create tests easier by providing us many features, remember the architecture we've been building ? 
Here it is :
1. Create a test suit.
2. Create tests.
3. Compare values ad display result (passed / failed) 

### How to use Jasmine ?
Let's get to know the files and some therminology first :
- Spec : test file itself.
- SupecRunner.html : By default we find : loading frameworks, code we wanna test, files containing the test.  
**☝🏻Note** : we renamed `SupecRunner.html` into `test.html` for simplicity.

### Add our own tests :
#### 1. Cleaning up phase :
1. Inside test.html delete : code by default ( everything but Jasmine frameworks )
2. Remove *src* and *spec* folders.

#### 2. Creating a test :

Create a test file `fileNameTest.js` per file `fileName.js` we wanna test from our project.  
**👍🏻 Good practice :** trying to match project folders architecture  
*Example:* if **'cart.js'** is inside **'data'** folder, let **'cartTest.js'** also inside a **'data'** folder)

**Let's move on to the most important functions and methods :**  
**1. Give the suit a name** => `describe('name' , () => {} )`  
Inside its inner function :  
**2. Create a test** => `it( 'description' , () => {} )`  
Inside its inner function :  
**3. Compare values and display result** => `expect(code to test).methods(...)`   
`expect()` returns an object.  
Object = has many methods to use.  
*ex*: `expect(...).toEqual(...);`  

We'll see many methods as we build our project together.  

#### 3. Once we created a test, how can we run it ?
By creating a `<script>` tag inside the `test.html` file.  
*Example :*
```JavaScript
<script src="moneyTest.js" type="module" ></script>
```
**👀 Notice :** We added `type="module"` cause we're importing the code to test from original files. 
Now all we have to do is open the html file using liveServer !  

#### What happends when a test file ?
Jasmine gives us a lot of details to help us fix the issue.  
Here an exemple of how it would look like :  
<img width="767" height="125" alt="Capture d&#39;écran 2026-06-18 195134" src="https://github.com/user-attachments/assets/629739aa-5efd-4739-83bd-cd5241b867be" />

### Problem : Testing REAL values :  introducing 'mock'

**🎬 Scenario :** We wanna test `addToCart()`, a function which adds a product to a cart.  
When adding a product to an **empty** cart, we expect the overall length to be equal to 1.  
But 'cart' variable changes, it's not fixed = test fails just because the length is different from what we expected, not because the code didn't work !  

This is where **Mock** comes in ! :D 
**Mock** = replace a method with a fake version.  

#### How Mocking works ?
WE decide what the method do/return.
At the top of the test `it()` add `spyOn()` code :

*Example syntax :*
```JavaScript
spyOn(Object to mock, string method ).and.callFake( () => {
//Code to override the 'method'
} );
```
In our 'empty cart' case, once the function calls load from localStorage using the method `getItem()`, we rather want it to return an empty cart : `return JSON.stringif([]);`.  
Here's how the code would look :  
```JavaScript
spyOn(localStorage, 'getItem').and.callFake( () => {
    //Control what WE want the localStorage to return >:D
    return JSON.stringify([]);
});
loadFromStorage();
```
**👀 Notice :** Let's talk about this `loadFromStorage();`, why is it important to load again ?  
Order matters ! We need to tell the computer : we mocked the method first using `spyOn()` THEN call it. 
So what happends when `loadFromStorage()` is called ?  
It runs `localStorage.setItem()` from the original code, but we mocked it here, so calling it make it returns EXACTLY what we wrote (empty array) !  

#### Saving problem :
Inside the function `addToCart()` we save to localStorage.  
But we DON'T want the test to modify the **actual** 'cart' variable.  
**Solution :**  
Mock LocalStorage.setItem() too !  
What we want : no saving.   
What we write : make it do nothing (no return) !  

```JavaScript
spyOn(localStorage,'setItem');
```

#### How to check a method was called ?
What if I wanted to make sure the cart was actually saved in localStorage ?  
Saved in localStorage = called the method `.setItem()`.  
**Solution :**  
`spyOn()` records every time a method is used.  
🗒️**Reminder :** `Expect()` returns an object with many methods.  
A useful method for this situation is `.toHaveBeenCalledTimes()`.  
Full Syntax :  
```JavaScript
expect(localStorage.setItem).toHaveBeenCalledTimes(1);
```

### Unit Test Vs. Integration Test :

- **Unit test :** testing ONE piece of the code. This is what we've been doing until now.
- **Integration Test :** tests many units/pieces of code working together.

Example of an integration test :
Testing `renderOrderSummary()` = uses *multiple* functions and libraries to render the page.  
Let's go through this together :

#### What test cases (it()) should we create ? 
When testing the page, we have 2 things to test :  
1. How it looks.  
2. How it behave.
