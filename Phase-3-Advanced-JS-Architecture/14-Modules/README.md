# 📓 Lesson 13: Modules 

## 👀 Overview
This notes is an introduction to module, their implementation workflows and real-world application inside e-commerce project.   
You'll also find a set of technical challenges I encountered during development, "why" they are a problem and their fix  
Studying problems and their fixes are the best way to learn :D  

## 🗺️ Table of Contents
1. [🧩 The Module Paradigm: Scope Isolation](#1-the-module-paradigm-scope-isolation)
2. [📦 Import & Export Blueprints](#2-import--export-blueprints)
3. [Me VS Exercises](#3-exercises-review-&-personal-notes)

## 1. The Module Paradigm: Scope Isolation

### 🧠 The Core Concept
Modules = better way to organize our code.  

**Before Modules :**  
By default, JavaScript **files** share a **single** huge globale scope.   
In other words, every script file you call using <script> element is converted into a giant single one.  

**What's the problem ?**  
Naming conflict :)  
If you use a variable in a certain file, you can NO LONGER use it for other purposes, even in a different script file :c  

**How it works ?**
Don't load the file using the `<script>` tag in your HTML file.  
Yeah, that's all :o

### ⚖️ The Benefits : after modules 
- **Zero Naming Conflicts:** Multiple files can use identical variable names, yay !
- **Order Indepedence** We no longer need to worry care in which order we load the `<script>` tags inside our HTML file !

## 2. Import & Export Blueprints
**Problem :** Cool, but what if we actually needed a variable from ANOTHER file ?  
**Solution :** Let our files communicate together using import & export :D  
To allow our isolated module files to communitcate, there's 3 steps :  
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
Some generated HTML don't need the `matchingProduct` variable, like the quantity, it can be found  directly inside the cart items' properties `cartItem.quantity`.  

```HTML
<span>
  Quantity: <span class="quantity-label">${cartItem.quantity}</span>
</span>
```

## 3. exercises review & personal notes
Let's go through my struggles and thought process together ;.)
⚠️ NOTE ! These code snippets ALONE aren't functional, they're parts of a bigger project, I placed them here just to make the examples clearer.  

### He asked me " when page loads, do 'x' "
I was confused at first about whether I should place it somewhere specific in the file, but nope !

#### 💡Solution :
1. Go into the JavaScript file of this page (ex : if you're working for `amazon.html` go for  `amazon.js`).  
2. Just create/invoke a funtion (the one that handles 'x' )right there on its own line.

#### 💻 Code
*Example* : When page loads : update cart quantity

```JavaScript
//On a random line :
updateCartQuantity();
```

### Why quantity of items (in the header) is not updated when deleting a product in the cart ?

#### 🎬 Scenario :
I was deleting the products from the page, the cart in memory was being updated perfectly but the total number of items in the header section remained the same..until I refreshed the page again !  

#### 🎯 Where's the issue ?
The fact that the numbers only updated upon refreshing meant two things :
1. The cart data was changing successfully => No problem with the cart !  
2. When the page loaded fresh, it read the right numbers => no problem with display AFTER refresh
Hmm, do you see it ?  
Loaded = reading the script file `checkout.js` again !  
And that script file is what contains the code to compute the total quantity in the cart.  

#### 💡Solution :
The browser reads the script file + calculates the total ONCE on page load.  
If I wanted it to update the total number of items *ANOTHER* time, I had to manually trigger that recalculation.  
It means : running it each time the user deletes a product was deleting a product or more generally : whenever I update product numbers on the page (what we'll do later on with 'update' button).  

```JavaScript
//Set event listeners to 'delete' button of EACH (ALL) product
document.querySelectorAll('.js-delete-link')
  .forEach((link) => {
    link.addEventListener('click', () => {
      //1. Remove from cart
      const productId = link.dataset.productId;
      removeFromCart(productId);

      //2. Remove container from the web page
      const container = document.querySelector(`.js-cart-item-container-${productId}`);
      container.remove();

      //3. Update the header total items live !
      updateCartQuantity();
    });
  });
```

**👀 Notice** at *step 3* how I invoked `updateCartQuantity()` right inside the delete event listener !  
Now every single click forces the header to recalculate and stay perfectly in sync with our data
   
### Making 'update' on product button functional
Let me just explain the solution he was following :

1. Add event listener to ALL 'update' buttons `document.querySelectorAll('.js-update-link')`
2. Get the Exact product we're modifying using its id, we attached the id info to the update link, to get it once we call it from `const productId = link.dataset.productId;`
4. Select container of the whole product `document.querySelector(`.js-cart-item-container-${productId}`);`
5. Add a class to container `classList.add('is-editing-quantity')`.

#### 💻 Code
```JavaScript
//Make 'update' button interactive
document.querySelectorAll('.js-update-link')
  .forEach(link => {
    link.addEventListener('click', () => {
      const productId = link.dataset.productId;

      //Find container of product to update, add class = is-editing-quantity
      const container = document.querySelector(`.js-cart-item-container-${productId}`);
      container.classList.add('is-editing-quantity');

    });
  });
```
