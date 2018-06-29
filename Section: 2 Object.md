## Exercise: Stopwatch ##

### Requirement: ###
Create a stop watch object with **Start(), Stop(), Reset()** methods. And user should be enable call these method once stop watch object created. Meanwhile there will be validation to **check** if watch is **already Start/Stop**. If current request violate the validation then show error message. 
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
