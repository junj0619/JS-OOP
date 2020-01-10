## Getting Started ##  
 
### 1.What is OOP? ###

#### What is Object-oriented Programming(OOP)? ####

Object-oriented programming (OOP) is a popular programming paradigm or style of programming. It’s been around since ‘70s, but unlike tools and frameworks that come and go, OOP is still very relevant today. That’s because it’s not a programming language or a tool. It’s a style of programming.
  

#### Why learn OOP? #### 

OOP helps you manage and reduce complexity in software by building re-usable building blocks (objects). Properly designed objects provide a simple interface and hide the unnecessary complexity from the outside, just like a DVD player! A DVD player has a complex logic board on the inside and a few buttons on the outside. When you press the play button, you don’t care how all those microchips talk to each other.


#### Object-oriented programming helps you: #### 

* Manage and reduce complexity
* Eliminate redundant code
* Build re-usable building blocks
* Write cleaner code


### 2.Four Pillars of OOP? ###

Before Object-Oriented Programming, We had **procedure programmming** divided a program into a set of fucntions. so you have data stored in a bunch of variables and functions that operate on the data. This style of programming is very simple and straight forward but as your programs grow, you end up with a bunch of functions that all over the place. You might find yourself copying and pasting line of codes over and over to make a change to one function and then several other functions break. That's what people call spaghetti code, there is so much interdependency in all these functions it becomes problematic.   

Object-Oriented Programming came to sovle this problem, in  Object-Oriented Programming we combine a group of related variables and functions into a unit. We call that unit an object. We refer to these variable to **properties**, and the functions as **methods**.

For example the localStorage in your browsers. Every browsers has a local storage object that allows you store data locally. This localStorage object has a **property** like **length** which returns the number of objects in the storage, and **methods** like **setItem()** and **removeItem()**. So in object oriented programming you group related variables, and functions that operate on them into objects. And this is what we call **Encapsulation**.

Here we have 3 variables baseSalary, overtime and rate. Below this, we have a function to calucate the wage for an employee.
We refer this kind of implementation as **procedure** so we have variables on one side and functions on other side, they are hard to decouple.

```javascript
let baseSalary = 30000;
let overtime = 10;
let rate = 20;

function getWage(baseSalary, overtime, rate) {
    return baseSalary + (overtime * rate);
}

```

Now let's see **object-oriented** way to solve this problem.

```javascript

let employee = {
    baseSalary : 30000,
    overtime : 10,
    rate : 20,
    getWage : function () {
       return this.baseSalary + (this.overtime * this.rate);
    }
};

employee.getWage();

```
**Now why is this better?**  
First of all let's look at get wage function. This function has no parameters. In contrast, in a procedural example, our getWage function has 3 parameters. The reason this implementation don't any parameters, is because all these parameters are actually modeled as properties of this object. All these properties and getWage() function are highly related, so they are part of one unit. So one of the symptoms of procedural code is functions with so many parameters. When you write code in an object-oriented way, your functions end up having fewer and fewer parameters. The fewer the number of parameters the easier it is to use and maintain that function. So that is **Encapsulation**.

#### Encapsulation ####
Group related properties and methods together. This will reduce complexity.  

**Benefits:**
1) Reduce Complexity
2) Increase reusabiliy

#### Abstraction ####
Hide the detail(properties and methods) and complexity and show only the essential

**Benefits:**
1. Simpler Interface/Reduce Complexity
2. Reduce the Impact of Change/Isolate impact of changes

#### Inheritance ####
1. Eliminated Reduantant Code

Here is example:  
Think about of HTML elements **TextBox, Select, CheckBox**. All these elements have some commons **Property likes hidden, innerHTML** and **Methods like click() and focus()**. Inside of redefine every properties and methods in all HTML elements. Inside we can define a generic HTMLElement and let all HTML elements inherit it. So Inheritance helps us eliminated reduantatn code.


#### Polymorphism ####
1. Refactor ugly switch/case statements


__Poly__ means __**MANY**__, __morph__ means __**FORM**__ so Ploymorphism means many forms in OOP it helps us to get rid of long **if** and **else** and **swich** statements. So back to our previous example all these HTML elements shoud have ability to render it on the page. But the way to render is difference than each others. If you want to render mutiple HTML elements in procedure way. Then you have to come up with following code structure.


In Procedure way to render multiple HTML elements:

```javascript
switch(type) {
    case 'select': renderSelect();
    case 'text': renderTextBox();
    case 'checkbox': .....
    case ...
    case ...
    case ...
}
```

But with OOP we can implement this render() methods in each of HTML element. And render() will behave differently depends on type of object we are referencing. So we can get rid of the ugly switch case inside using **element.render()**.

<pre>
                HTMLElement                 
       _____________|_____________
      |             |             |
  ____|____     ____|____     ____|_____   
 | TextBox |   | Select  |   | CheckBox |
 | render()|   | render()|   | render() |                              

 </pre>

### 3.Setting Up the Development Environment ###
1. VS Code
2. Install Live Server
3. Create index.html and index.js
