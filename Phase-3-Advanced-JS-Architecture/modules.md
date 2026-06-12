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
