---
layout: note
title: JavaScript: How to call multiple functions in parallel with async/await?
permalink: parallel-run-with-async-await
---
Let us suppose, we have four asynchronous functions which we want to call in parallel. 

These four functions are:

```javascript
doAsyncTaskOne = ()=> {
    // some async operation here
    // and return a promise
};

doAsyncTaskTwo = ()=> {
    // some async operation here
    // and return a promise
};

doAsyncTaskThree = ()=> {
    // some async operation here
    // and return a promise
};

doAsyncTaskFour = ()=> {
    // some async operation here
    // and return a promise
};
```

It is a two step process. 

First, call these methods and store the returned promises. This will make all four call instantly. However, promises will not resolve just yet.

Second, *await* for these promises to resolve.

```javascript
async function runInParallel {
    const taskOneResult = doAsyncTaskOne();
    const taskTwoResult = doAsyncTaskTwo();
    const taskThreeResult = doAsyncTaskThree();
    const taskFourResult = doAsyncTaskFour();
    return [
        await taskOneResult,
        await taskTwoResult,
        await taskThreeResult,
        await taskFourResult
    ];
}
```

Note: Even if one promise is rejected , an error will be sent.

Pro Tip: With async/await, use try and catch to handle any error.

Also, if you were to do same thing with promises instead of async/await, you can do following:

```javascript
function runInParallel {
    return Promise.all ([
       doAsyncTaskOne(),
       doAsyncTaskTwo(),
       doAsyncTaskThree(),
       doAsyncTaskFour()
    ])
}
```

