# 📓External Libraries

## 🗺️ Table of Contents
- [External Libraries](#1-external-libraries)

## 1 External Libraries :

### Overview :
External library = code outside our project.  
Other developers write some code then put it on the internet.  
And we can actually loads their code into our project !  

### How to load it ?
Add a `<script>` tag at the end of the html page.   
Use the `src` attribute to past the URL in.  
```HTML
<script src="https://unpkg.com/supersimpledev@8.5.0/dayjs/esm/index.js"></script>
```
Now whatever is in the code, we can run it.  

**👀 Notice :** If you look into the code we're uploading it can look cursed..(no spaces at all :o )   
It's just something called **minification**  
What's the purpose of minification ?  
Compressing the code makes the loading process from the internet easier.  

### Problem with script tags
May cause naming conflics if the library contains names of variable we're already using in our project

Solution ? => Modules :D  
To use : modules + libraries  
We use ECM version of JavaScript  
ECM version = JavaScript + extend in front of its functions  

### ECM vs JavaScript  
JavaScript
```JavaScript
function hello() {
  console.log('hello');
}
```

ECM : add `export`
```JavaScript
export function hello() {
  console.log('hello');
}
```

Since the ECM version exports its variable and function  
All you do is importing it from the source = internet URL.  
At the top of the JavaScript file type :  

```JavaScript
import dayjs from "https://unpkg.com/supersimpledev@8.5.0/dayjs/esm/index.js"
```
**👀 Notice :** No curly brakets `{dayjs}`?   
It's called the default export  
Used when we only wanna export one thing = make the syntax cleaner  
It's up to you 🫵🏻 which version to use.  

## dayjs library & documentation

Now that we imported our external library, the best way is to read the **documentation**  
Here what we've seen in the course:  

dayJS library creates a function : dayjs();  
Returns an object containing today dates  
Dayjs() has methods : 

### Increase the number of days ?  
`.add(1st , 2nd) `  
- 1st :  nbr of days  
- 2nd : what format ?  

*Example :*  
```JavaScript
dayjs().add(7,'days');
```
7 days after today

### Need to display the date in an easy to read format ?
(Get rid of the object format)  
`.format()` :  

Takes date and converts it into a **string** using given format  
How to pass the format in ?  
Using the table present in the documentation   
*Example*
```JavaScript
dayjs().format('dddd, MMMM D');
```
- `dddd` full weekday name
- `MMMM` full month name
- `D` numeric day of the month

## Delivery options e-commerce project
Goal : Clicking an option = changes delivery date + price
Pseudo-code :
1. Get today's date.
2. Do calculation : adding 'x' days.
3. Display the date in easy-to-read format.

### 1. Save data : 
What data do we need (what changes when interacting )?  
1. Delivery date.
2. Price.

Where to save those ?  
We could save the options in the cart...BUT it would be duplicated.   
Instead we save them seperatly then save an ID that points to this delivery option : Normalizing the data.  
1. Create a new script file 'deliveryOptions' in `data` folder.
2. Create an array containing the options as objects.

```JavaScript
export const deliveryOptions = [{
  id: '1',
  deliveryDays: 7,
  priceCents: 0
}, {
  id: '2',
  deliveryDays: 2,
  priceCents: 499
}, {
  id: '3',
  deliveryDays: 1,
  priceCents: 999
}]
```

### 2. Generate the HTML
Follow these 3 steps :  
1. Loop through deliveryOptions
2. For each option : generate some HTML
3. Combine the HTML together

**Step 1 & 2** orderSummary.js file Inside a function : loop through the array + generate the HTML (the orangist code)

**Custom delivery date :**  
Let's generate a CUSTOM date per deliveryOption !  
At the top inside the function :

```JavaScript
  const today = dayjs();
  const deliveryDate = today.add(deliveryOption.deliveryDays, 'days');
  const dateString = deliveryDate.format('dddd, MMMM D');
```
**Custom price :**   
Using ternary operator : 
```JavaScript
const priceString = deliveryOption.priceCents === 0
        ? 'FREE'
        : `$${formatCurrency(deliveryOption.priceCents)} -`;
```

Now that we have our date `dateString` and price `priceString` variables, we insert them into the generated HTML.That's we're doing in step 3 :D

**Step 3 : Combining the HTML**  
Created an accumulator patter (variable =+ generated HTML) that the function returns at the end
We then inserted the function into the generated HTML for each product :
Here we passed matching product variable as a param, cause it's needed 

```JavaScript
html += `
    <div class="delivery-option js-delivery-option"
      data-product-id="${matchingProduct.id}"
      data-delivery-option-id="${deliveryOption.id}"
      >
      <input type="radio"
        ${isChecked ? 'checked' : ''}
        class="delivery-option-input"
        name="delivery-option-${matchingProduct.id}">
      <div>
        <div class="delivery-option-date">
          ${dateString}
        </div>
        <div class="delivery-option-price">
          ${priceString} Shipping
        </div>
      </div>
    </div>
```
**👀 Notice :** `name="delivery-option-${matchingProduct.id}">` we set a different name for each set of product, name attribute is what determine what radio element are from the same set or not.

## Problem : Empty delivey options
Goal : We want to select one by default.
Which one should be checked ?  
The one that matches the deliveryOption id in the cart => Let's find it !  

```JavaScript
const isChecked = deliveryOption.id === cartItem.deliveryOptionId;
```
Now remember that `checked` is a property inside `<input>` tag.  
Property : means its value = string.  
This line of code is setting a check on the right delivery option among the 3 proposed.  

```JavaScript
<input type="radio"
${isChecked ? 'checked' : ''}
//Code...
>
```

### Match Selected date on top

From the cart, we only save the delivery option id; we'll use it.  
1. Get id from the cart item.
2. Find matching id in deliveryOptions array.
3. Format the right date.
4. Place date variable on the product generated HTML.

## 3. Make it interactive = event listeners tiimme :D

Goal : When selecting a different option it updates the date  
Pseudo-code (steps to follow):
	1. Update deliveryOptionId in the cart array
	2. Update the page (HTML) date up the product to match the selected option

### 1. Update deliveryOptionId in the cart
Create a function in 'cart.js' that does :
	1. Loop through the cart to find the product (using productId)
	2. Update the deliveryOptionId of the product (using newDeliveryOptionId)
In order to do so the function needs 2 params : 
	1. productId we're updating 
	2. New delivery Option

When adding event listeners invoking the function inside it  
How can we get its two parameters: **productId**, **newDeliveryOptionId**.  
We attach it to element we're getting using the DOM.  
Extract from the 'element' it inside the function :  
And now we can fill our function's parameter, yay :D  

### 2. Update the page :

Problem with updating using the DOM : update it one-by-one what make it easy to forget something..
Best practice is to re-render the page each time we modify something.  
How ?  
Place all the generated HTML inside a function  
Instead of using the DOM to update the page directly (like we did up here)  

#### Why placing the event listener INSIDE render function ?
When regenerating the HTML, we're wiping out the old event listener = we need to add them again.

## Regenerate all HTML = technique MVC
MVC : project is split into 3 parts :
	1. Model : code that saves and manages the data (ex : cart.js file)
	2. View : Takes the data and displays it on the page (ex : HTML in checkout.js)
	3. Controller : runs code when interacting with the page (ex : event listeners in checkout.js)

They interact with each other in a loop
	1. Use Model to generate the View (generated HTML from cart)
	2. When interacting with the View it will run the Controller (interacting with the page : runs some code)
	3. Controller will update the Model (data)
	4. Use the updated Model to regenerate the View
### Why use MVC ? 
This techniques makes sure the page always matches the data
Design pattern = a way to organize our code 
Many javaScript frameworks are based on MVC

