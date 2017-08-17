# JavaScript
## Closures
Closure is another important concept in JavaScript and understanding this can be really helpful while building javaScript applictions.
A closure is a combination of a function bundled together with references to its surrounding state(**lexical environment**).
That is  a closure gives you access to an outer function’s scope from an inner function. All this might sound a bit confusing but it is better understood as you read further.
Now we'll look at an example where we will actually see how these closures may be helpful.
Take a simple example of implementing a counter function. It can be implemented easily by running the following code.
```
var count = 0;//Global Variable
function counter(){
  count = count + 1;
  return count;
}
```
Now run ```console.log(counter()) //outputs 1```
Again run ```console.log(counter()) //outputs 2```
It seems to work perfectly and is pretty straight forward. Well, although this might work for this small program but if you wish to right a large piece of code with many people contributing and using the same variable counter you will surely run into a problem. The other possibility is using a local variable.

```
function counter(){
  var count = 0;//local variable
  count = count + 1;
  return count;
}
```
In this case if you run ```console.log(counter())``` you will see that it always outputs 1. This is because our variable is always reassigned to 0 whenever we call the function.

Thats where closures come in.

We define the function in the following manner
```
function makeCounter() {
  var count = 0;
  function counter() {
  count = count + 1;
  return count;
}
  return counter;
}
```
Then we run the following commands
```
var doCount = makeCounter();
console.log(doCount());//outputs 1
console.log(doCount());//outputs 2
```
At first glance, it may seem unintuitive that this code still works. In some programming languages, the local variables within a function exist only for the duration of that function's execution. So after makeCounter() is called the variable named count can get destroyed and may no longer be accessible. But in Javascript that's not the case.

This is beacause functions in JavaScript form closures(functions along with the lexical environment). This environment consists of any local variables that were in-scope at the time that the closure was created. In this case when we call makeCounter, it creates a counter function and returns it along with an environment containing the free variable (Actual reference to the count variable , not a copy) count. In other words, it creates a closure. The function returned from makeCounter is stored in doCount. So whenever we call doCount it looks for a variable named count in the lexical environment and retrieves its value.

So this is what basically a closure is. However there are many applications of closures and if you are interested you can read further in  the [documentation](https://developer.mozilla.org/en/docs/Web/JavaScript/Closures)
