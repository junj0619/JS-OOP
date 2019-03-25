
## 2- Object Literals ##
Creating an Object with Object Literals is an issue only if that Object contains behaviors(methods)

Solution: using Factory/Constructor Function

```javascript
const circle = {
    radius: 10,
    location: {
        x: 1,
        y: 1
    },
    draw: function () {
        console.log('draw a circle');
    }
};

circle.draw();
```
## 3- Factory Function ##
1.Factory Function must have return keyword.
2.Using Factory Function to create an object don't use new keyword

```javascript
function createCircle(radius) {
    return {
        radius,
        draw: function () {
            console.log('draw a circle with radius: ' + this.radius);
        }
    }
}

const circie1 = createCircle(1);
circie1.draw();
```

## 4- Constructor Function ##
1.Constructor function using Upper Case as function name
2.Constructor function don't use return keyword
3.Use this keyword to assign property
4.Use new keyword for creating object by using Constructor Function

**What happen when use new keyword to create an object?**
1.An empty object will be create first
2.Point all this. properties and methods to this empty object
3.Return the object from this function
```javascript
function Circle(radius) {
    this.radius = radius,
        this.draw = function () {
            console.log('draw a circle with radius: ' + this.radius);
        }
}

const circle2 = new Circle(2);
circle2.draw();
```

## 5- Constructor Property ##
Every Object has a Constructor property. Constructor property that is referencing the function that create object




## 6- Functions are Objects
Constructor property that is referencing the function that create object Build-In Constructor is called Function() when we declare a function using this syntax. Internally JavaScript engine will use this Function() Constructor to create the Object.

```javascript
const CircleObj = new Function('radius', `
    this.radius = radius;
    this.draw = function() {
        console.log('draw');
    }
`);

const another = new CircleObj(1);
another.draw();

// same as const circle = new Circle(1);
Circle.call({}, 1);
Circle.apply({}, [1]);
```


## 7- Value Types vs Reference Types ##  
<pre>
    Value Types vs  Reference Types
 -----------------------------------
     Number     ||  Object
     String     ||  Function
     Boolean    ||  Array
     Symbol     ||  
     undefined  ||
     null       ||
 ------------------------------------
</pre>  
  Primitives are copied by their value.  
  Objects are copied by their reference.

```javascript
let x = 10;
let y = x;

x = 20;
//result: x = 20, y = 10;

let x = { value: 10 };
let y = x;
x.value = 20;
//result: x.value = 20, y.value = 20

//---------------------------------------//
let x = 10;

function increase(x) {
    x++;
}

increase(x);
console.log(x);
// x = 10

//------------------------------------//
let obj = { value: 10 };
function increase(obj) {
    obj.value++;
}
console.log(obj.value);
// obj.value = 11
```

## 8- Adding or Removing Properties 
In JavaScript we can dynamic add or delete an Property from an Object.  We can use dot notation or bracket notation to access object property.

```java
const circle8 = new Circle(1);
circle8.location = { value: 10 };
circle8['location'] = { value: 10 };
delete circle8.location;
delete circle8['location'];

//If we don't know key ahead of time. we can use bracket notation.
//We also can use special character in the key in bracket notation
let propertyName = "location";
propertyName = "location-new";
circle8[propertyName] = { value: 10 };
```

## 9- Enumerating Properties 
```javascript
const cirObj = new Circle(1);
for (let key in cirObj) {
    if (typeof cirObj[key] !== 'function') //get only property not method
        console.log(key, cirObj[key]);
}

//get all object keys
const keys = Object.keys(cirObj);

//check if property exists in an Object
if ('radius' in cirObj) {
    console.log('Cricle has a radius.');
}
```

## 10- Abstraction 
```javascript
/* Hide the detail only show the details */
function Circle(radius) {
    this.radius = radius;
    this.defaultLocation = { x: 0, y: 0 };
    this.computeOptimumLocation = function (factor) {
        // ...
    }
    this.draw = function () {
        this.computeOptimumLocation(0.1);
        console.log('draw');
    };
}
```

## 11- Private Properties and Methods ##

```javascript
/* Change defaultLocation property and computeOptimumLocation method only avaiable to Circle object itself */
function Circle(radius) {
    this.radius = radius;
    let defaultLocation = { x: 0, y: 0 };
    let computeOptimumLocation = function (factor) {
        // ...
    }

    this.draw = function () {
        computeOptimumLocation(0.1);
        console.log('draw');
    }
}
```

## 12- Getters and Setters ##
```javascript
/* 1st way to implement getter of defaultLocation */
function Circle(radius) {
    this.radius = radius;
    let defaultLocation = { x: 0, y: 0 };

    this.getDefaultLocation = function () {
        return defaultLocation;
    }
    this.draw = function () {
        console.log('draw');
    }
}

/* 2nd way to implement getter */
function Circle(radius) {
    this.radius = radius;
    let defaultLocation = { x: 0, y: 0 };

    Object.defineProperty(this, 'defaultLocation', {
        get: function () {
            return defaultLocation;
        },
        set: function (value) {
            if (!value.x || !value.y) {
                throw new Error('Invalid location.');
            }

            defaultLocation = value;
        }
    })

    this.draw = function () {
        console.log('draw');
    }
}
```



## Exercise: Stopwatch ##

### Requirement: ###
Create a stop watch object with **Start(), Stop(), Reset()** methods. And user should be enable call these methods after stop watch object is created. Meanwhile there will be validation to **check** if watch is **already Start/Stop**. If current request violate the validation then show error message. 
User also can call **duration** property to check the stopwatch interval.     
Take **30 mins** to finish this requirement with clean design code.

**By me:**
```javascript
function StopWatch() {

    let isStart = false;
    let isStop = false;
    let startTime;
    let endTime;

    this.start = function () {
        if (isStart) {
            throw new Error('Can not start.');
        }
        startTime = new Date();
        isStart = !isStart;
        // console.log(startTime);
    }

    this.stop = function () {
        if (isStop) {
            throw new Error('Can not stop.');
        }
        endTime = new Date();
        isStop = !isStop;
        // console.log(endTime);
    }

    this.reset = function () {
        isStart = false;
        isStop = false;
        startTime = null;
        endTime = null;
    }

    Object.defineProperty(this, 'duration', {
        get: function () {
            return (startTime !== undefined && endTime !== undefined) ? 
            (endTime.getTime() - startTime.getTime()) / 1000 : 0;
        }
    });
}
```



**Solution:**

```javascript
function StopWatch() {
    let startTime, endTime, isRunning = false, duration = 0;

    this.start = function () {
        if (isRunning) {
            throw new Error('Watch is running. Can\'t start again.');
        }
        isRunning = !isRunning;
        startTime = new Date();
    }

    this.stop = function () {
        if (!isRunning) {
            throw new Error('Watch is not running. Can\'t stop it.');
        }
        isRunning = !isRunning;
        endTime = new Date();
        duration += (endTime.getTime() - startTime.getTime()) / 1000;
    }

    this.reset = function () {
        isRunning = startTime = endTime = duration = 0;
    }

    Object.defineProperty(this, 'duration', {
        get: function () {
            return duration;
        }
    });
}
```

**Summary**  
Compare to Mosh's solution I found few things are not implemented properly on my solution.
1. Duration is not added on previous duration value
2. The validation to check isStart/isEnd can be simplified
3. Duration Getter logic doesn't have to check startTime/endTime undefine if we initial them at begining 
4. Calculation of duration can be implemented in Stop() function 
