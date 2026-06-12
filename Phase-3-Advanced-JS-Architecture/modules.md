# 📓 Lesson 13: Modules 

## 👀 Overview
This notes is an introduction to module, their implementation workflows and real-world application inside e-commerce project we can use them.  
You'll also find a set of technical challenges I encountered during development, "why" they are a problem and their fix  
Studying problems and their fix are the best way to learn :D  

## 🗺️ Table of Contents
1. [🧩 The Module Paradigm: Scope Isolation](#1-the-module-paradigm-scope-isolation)
2. [📦 Import & Export Blueprints](#2-import--export-blueprints)

## 1. The Module Paradigm: Scope Isolation

### 🧠 The Core Concept
Modules = better way to organize our code.  

**Before Modules :**  
By default, JavaScript **files** share a **single** huge globale scope.   
In other words, every script file you call using <script> element is converted into a giant single one.  

**What's the problem ?**  
Naming conflict :)  
If you use a variable in a certain file, you can NO LONGER use it for other purposes, even in a different script file :c  

### ⚖️ The Benefits : after modules 
- **Zero Naming Conflicts:** Multiple files can use identical variable names, yay !
- **Order Indepedence** We no longer need to worry care in which order we load the `<script>` tags inside our HTML file !

## 2. Import & Export Blueprints
**Problem :** Cool, but what if we actually needed a variable from another file ?  
**Solution :** Let our files communicate together using import & export :D  
To allow our isolated module files to communitcate, we have 3 steps :  
1. Add the property `type="module"` to the `<script>` tag related to the file **importing** from other files.
2. Export from original files.  
3. Back into module file, at its TOP, import it.  

### 💻 Technical Blueprint & Syntax

#### Step 1 : Add type, end HTML file
```html
<script src="scripts/checkout.js" type="module"></script>
```

#### Step 2 : Named export 
```JavaScript
export function formatCurrency(...) {
  //Block of code..
}
```
#### Step 3 : Back into module file Explicit Import (checkout.js)
👀 **Note :** We need to tell the computer where to find the folder using a **path**
**Path syntax :**  
* "." means current folder.
* ".." means move up ONE folder level (ex : "../../" means TWO level).
```JavaScript
import { formatCurrency } from '../utils/money.js';
```

### 🛑 Architectural Conditions
**1. Header rule :** all `import` statements MUST sit at the absolute top of the file.  
**2. Environment Restriction :** Modules won't work if you open the HTML file directly in a browser using local file system (from the files you find on your computer c: ). Must use a local development server like : VS Code Live Server

## 3. Display products on checkout page:
I'll take you with me through my thought process while trying to figure how to display the product saved inside a cart array, and display it on the website !  

**Problem :** Inside cart, we only save id & quantity of each product, but the checkout page displays way more details about each product !!    
Those details are saved in `product.js` file.    

**So, 2 information to keep in mind :**  
Checkout items (product in the cart) are in `cart.js`.  
Products details are saved in `product.js`.  

### 💻 Technical Blueprint & Syntax
**How can we connect between the two ?**
```JavaScript
cart.forEach((cartItem) => {
  //Get the cart id :
  const productId = cartItem.productId;

  //Find products details from product.js
  let matchingProduct;

  products.forEach((product) => {
    if (productId === product.id) {
      matchingProduct = product;
    }
  })
```

1. Save the id of each item in the cart `const productId = cartItem.productId;`.
2. Import products from products.js `import { products } from "../data/products.js";
`
3. Looping through the list of all products (products array), we seek a matching id.
4. Once found we save it in a variable `matchingProduct = product;`
5. `matchingProduct` now contains all the details about the current item in the cart = use it to generate the HTML !

**⚠️Beware**  
Some generated HTML don't need the `matchingProduct` variable, like the quantity, it can be found directly inside the cart items' properties `cartItem.quantity`.  
```HTML
<span>
  Quantity: <span class="quantity-label">${cartItem.quantity}</span>
</span>
```
