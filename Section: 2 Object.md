<h2>Exercise: Stopwatch</h2>

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
