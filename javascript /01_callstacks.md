# How Js Executed
Before getting into Explanation its better to understand what matters: \
When we run JS code, it makes an execution context. It is composed of memory phase and execution phase. 

```js
let me = {name: "something", age: 10, area: "local"}
console.log(me.name);

// It creates a execution context
// In memory phase, it stores variable me with value undefined
// In execution phase, it points me to the object in heap memory
// It loads function in call stack
// After execution, the function gets removed from call-stack

```
In memory phase, Js engines scans entire script from top to bottom and variables, functions and classes are hoisted at local context. 
```js
name = "abcc";
console.log(name);
var name = "something";

// Here, Just after scan, name is hoisted then in execution phase name is assigned to "abc" then logged and again assigned to "something"

greetMe();

function greetMe(){
    console.log('Hello, How are you ?');
}
// function and classes are also hoisted to the top with entire body

console.log(name2);
let name2 = "pqrs";
// ERROR: 
// let and const are also hoisted to the top of scope but because of TDZ it cause referenceError

```
Now, In Execution phase variables are assigned with values and when a function is called, it create its own context in callstack after usage it gets automatically removed.\
CallStack is like when function is called it loads and executes, if it requires another function, it loads on top of it and so on and just after execution it gets popped out LIFO manner (Garbage collection) . \
If one function loads another function and so on, It may cause stack overflow. It also keeps track of code from where to execute to keep execution in correct order.\
```js

function sayHi(name){
    return `Hey, ${name}. WhatsUP?`
}

function greetUser(){
    console.log(sayHi("User"));
}

greetUser();

// Js stores function body in heap memory
// When function is called here, It loads greetUser body in callStack
// Now, greetUser loads sayHi function in memory
// After sayHi execution, it gets popped out of callstack
// Now greetUser is executed and gets popped out of callstack
```
Memory Heap is a place to store and write information. It is like when a variable, function or class is declared, the value is stored in memory with variables pointing on them. We can use them anywhere by pointing them.