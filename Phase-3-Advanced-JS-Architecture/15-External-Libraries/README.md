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

Sometime the code we're uploading looks cursed..(no spaces at all :o )   
It's just something called **minification**  
What's the purpose of minification ?  
Compressing the code makes the loading process from the internet easier.  

### Problem with script tags
May cause naming conflics if the library contains names of variable we're already using in our project

Solution ? => Modules :D
To use : modules + libraries  
We use ECM version of JavaScript  
ECM verion = JavaScript + extend in front of its functions  

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

```JavaScript
import dayjs from "https://unpkg.com/supersimpledev@8.5.0/dayjs/esm/index.js"
```
No curly brakets ?   
It's called the default export  
Used when we only wanna export one thing = make the syntax cleaner  
It's up to you whick version to use.  

## dayjs library & documentation

Now that we imported our external library.   
The best way is to read the **documentation**

dayJS library creates a function : dayjs();  
Returns an object containing today dates  
Dayjs() has methods : 

**Increase the number of days ?**  
.add(1st , 2nd)  
1st :  nbr of days  
2nd : what format ?  

*Ex :* `dayjs().add(7,'days')`
7 days after today

**Need to display the date in an easy to read format ?**
(Get rid of the object format)
.format() :

Takes date and converts it into a **string** using given format  
How to pass the format in ?  
Using the table present in the documentation  

## delivery options e-commerce
Goal : Clicking an option = change delivery date + price
Pseud-code :
1. Get today date.
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

