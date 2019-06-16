# Callback and Promises
Basic blog introducing you to callbacks and promises.

# Callbacks
In lame words, if functions take another function as arguments, then those kind of functions are called higher order functions which take in arguments as callback functions.
Why needed callbacks?
Basic reason, when we can't wait for one function to execute completely before going for the next function to execute, we use callbacks so that we can execute our functions asynchronously.
Confused!?..will be clear within 10 mins.
  
```
function first() {
  console.log(1)
}
function second() {
  console.log(2)
}
first()
second()
```

This is basic top bottom execution.The output is straight forward. First will produce **first function**  then  **second function.**

But if the  first function  contains some complex process like fetching data that may first have to request and may take few seconds and we need not want to wait .So we execute the  second function first  then the first function  .So the program would somewhat look like.

```
function first() {
  // Simulate a code delay
  setTimeout(function() {
    console.log(1)
  }, 500)
}
function second() {
  console.log(2)
}
first()
second()
```

Here you would see the method **setTimeout**  which delays the function by 0.5s.
So the output would be **2** then **1**.

**Now lets see how to create a callback**.
 As told earlier when one function is passed as an argument to another function we call it as a callback function .

```
function doHomework(subject) {
 alert(`Starting my ${subject} homework.`);
}
doHomework('math');
// Alerts: Starting my math homework.
```

This is a basic example of creating a function and passing parameter to it.
Now.

```
function doHomework(subject, callback) {
 alert(`Starting my ${subject} homework.`);
 callback();
}
doHomework('math', function() {
 alert('Finished my homework');
});
```

This code will print back to back :**first Starting my math homework**  then  **Finished my homework.**
CallBacks need not always be defined in our function call.It can defined anywhere in the code.

```
function doHomework(subject, callback) {
 alert(`Starting my ${subject} homework.`);
 callback();
}
function alertFinished(){
 alert('Finished my homework');
}
doHomework('math', alertFinished);
```

 The above code prints the same output as the former code.


# Promise:
A promise is  an object which can return synchronously from an asynchronous tasks.
Promise exist to manage asynchronous requests (meaning not waiting for other functions to execute when something is still executing) more effectively.
Promises actually has 3 states: pending, fulfilled, rejected.

**Basic syntax**
`new Promise(executor);`

here executor is a function which takes two paramters resolve and reject. The executor normally initiates some asynchronous work, and then once that completes, either calls the resolve function to resolve the promise or else rejects it if an error occurred. If an error is thrown in the executor function, the promise is rejected. 

Initially the state of the Promise is `pending`. 
If the executor calls the resolve, it's state becomes `fulfilled`.
If the executor calls the reject, it's state becomes `rejected`.

Whatever data we pass to `resolve`, will be accessible via `then`.

**So how to create a promise?**
A basic example of how to create a promise

```
const prom = new Promise(function(resolve, reject) {
  // Do something
  if (success) {
    resolve('success')
  } else {
    reject()
  }
})

prom.then(function(data) {
  console.log(data);
})
```
The output will be *successs*.
Here we have used es5 functions, but it will be easier if we used arrow functions.

So small example using arrow functions.

```
const myPromise = new promise((resolve, reject) => {
  setTimeout(() => {
    resolve('timeout')
  }, 2000)
})

myPromise.then(msg => msg.toUpperCase()).then(capMsg => console.log(capMsg))
```
As you see, in the first **then** I'm making the message upper case and returning it
and in the second **then** I'm console logging it.
OUTPUT: *TIMEOUT*

So here you see `then` are chainable. That is you can return in one `then` and get it in the 
next `then`.

Lets take a real example on how to fetch data and display it in console.
```
fetch('https://jsonplaceholder.typicode.com/users')
  .then(result => result.json) // converts binary results to json
  .then(json => console.log(json))
```

If you see the above code , you can see a method called fetch  which returns promise. This is a way of fetching data .The above data fetched has to converted to JSON and then the value is displayed in console.

A pictorial representation of how promises work.
![how promises work](https://mdn.mozillademos.org/files/15911/promises.png)



## Difference between promises and callbacks.
Promises are cleaner way of executing asynchronous tasks to synchronous tasks. And also provides a cleaner mechanism to catch error which callback cannot do.
It just makes the code more simpler.

## References

https://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/
https://medium.com/@theflyingmantis/callbacks-vs-promises-and-basics-of-js-80d3d1515e81

