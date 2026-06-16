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

