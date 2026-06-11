# 📓 Lesson 13: Amazon Project and Git intro

## Table of content :
1.Bref view on git\
2.Display data using JavaScript + examples

## What is git ?
A technology that let us track changes on our website\
Let us easily undo our changes !\
**Repository** a folder where changes are being tracked

## How to include JavaScript into our HTML ? 
We have to understand the **main** idea of JavaScript :\

**1. Save the data**\
Creating something in JavaScript that closely matches the data displayed on the web page\

*Example*\
Creating an array (products) of objects
```JavaScript
const product = [{
 //Code product one
  },
  {
 //Code product Two
  }
...
]
```
**2. Generate the HTML**

Instead of generating it manualy , we use the saved data into JavaScript\

*Example*\
We have our data saved inside the array products, it's cool, but still in JavaScript and we would like to display them on the webpage\
**How ? Just follow these steps :**\
- Loop through the array of items, generate a customized template string `...` HTML to each
- Inside the HTML file, go get a 'receptor' to contain the generated content from JavaScript

**What's an accumulator pattern ?**
When looping through an array, accumulating the result of each generation at each iteration inside a certain variable
Why ? So we can use this variable to show all the HTML content on the page at once !
*Example :*
```JavaScript
let productHTML = '';

products.forEach((products) => {
  productHTML += `
  //Generated HTML
  `
})
```
👀**Notice** how we declared `productHTML` outside the loop, what's inside a loop concern a single element if the array, outside all of them..\
🧠**Reminder** forEach() while looping through an array, takes a single element at a time, saves it into its function parameter (so we could treat each element individually)

### How to include data from other files ?
We have this case senario : a file containing already all the product objects\
Instead of manually adding them to the array one by one , let's import them from that file\
**How ?** Add a <script> element right above the file needing them\
**⚠️ <script> order matter :** think of it : which one needs the data from the files above ? => place that one last\

**3. Make it interactive**

Pretty self-explanatory = make our displayed data do stuff :D (ex : respond to events)



