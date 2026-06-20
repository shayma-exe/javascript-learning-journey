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
We explictly tell the computer to do these tests for us !

### How many test cases should we have :
- **Basic Cases :** Verifying expected behavior "Is the code working ?"
- **Edge cases :** Testing risky values "Can this same code do X ?" 

## 🛠️ Jasmine Setup & Directory Architecture

#### What's Jasmine ?
A testing framework that let us create tests easier by providing us many features to :
1. Create test suit.
2. Create tests.
3. Compare values ad display result (passed / failed) 

### How to use Jasmine ?
Let's get to know the files first :
- Spec : test file itself.
- SupecRunner.html : By default we find : loading frameworks, code we wanna test, files containing the test.  
**☝🏻Note** : we renamed `SupecRunner.html` into `test.html` for simplicity.

### Add our own tests :
#### 1. Cleaning up phase :
1. Inside test.html delete : code by default ( everything but Jasmine framworks )
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


