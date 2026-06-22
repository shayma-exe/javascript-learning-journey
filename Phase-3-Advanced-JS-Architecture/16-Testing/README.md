# 🧪 Web Application Testing with Jasmine
In this lesson, we'll learn how to use a framework to test the code of our project, implementing 'Unit' and 'Integration' tests.  
At the end you'll be able to understand those 'words', how a test work.  

---
## 📋 Table of Contents
- [Testing Fundamental Concepts](#-testing-fundamental-concepts)
- Simple Testing (before frameworks)
- Jasmine Setup & Directory Architecture
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
## 🛠️ Simple Testing (before frameworks)

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

### What's Jasmine ?
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

### How a page looks : 
Problem : the original HTML is placed on the page, but where do we place it for our test ?  
If we look closer at the rendering function from the source code, it places the HTML inside a class :  
```JavaScript
document.querySelector('.js-order-summary').innerHTML = cartSummaryHTML;
```
👉🏻 We need to create an element of the same class , inside our 'test.html' file !  
We create it into a container : `<div>` element.  
Why ?   
We don't want to modify our entire body element cause it contains the result of Jasmine tests (display page).  

*test.html*   
```JavaScript
<body>
  <div class="js-test-container"></div>
</body>
```

*orderSummaryTest.js*
```JavaScript
document.querySelector('.js-test-container').innerHTML = `
      <div class="js-order-summary" ></div>`
```
Inside the element holding the class `js-test-container`, we insert the class the function is calling/using to render the page.

renderOrderSummary() uses the cart = by default we load it from localStorage = mock `localStorage.getItem()` to control what's in the cart.  

Note : don't forget to add a `<script>` tag in test.html file to run the test.  

#### Why the test page looks ugly :c , no CSS or images?

<img width="651" height="1046" alt="image" src="https://github.com/user-attachments/assets/2015dded-7f16-4850-a0e7-637ce46a4873" />

We can't really use code to check if the page looks VISUALLY correct.  
Instead we can check the 'data' = products and quantities.  
This is what we'll do below.

#### 1. Test number of products :

1. Add a 'js' class to whole products containers in source code.
2. Use it to select into an `expect()`, it document.querySelector returns an array = has method .length
3. Test if 'length' is equal to 2.

*orderSummaryTest.js*
```JavaScript
expect(
      document.querySelectorAll('.js-cart-item-container').length
    ).toEqual(2);
```

#### 2. Test quantity of a single products :
1. Add 'custom' classes to product quantity containers
2. Select product's quantity by product's id
3. innerText = get only the text inside the elements
4. There's a bunch of text : we want it to contain 'Quantity: 2' without minding about the others = use toContain() method.


```JavaScript
expect(
  document.querySelector(`.js-product-quantity-${productId1}`).innerText
).toContain('Quantity: 2');

expect(
  document.querySelector(`.js-product-quantity-${productId2}`).innerText
).toContain('Quantity: 1');
```
