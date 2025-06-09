---
title: Telegram Archive – Schriften Channel
tags: [telegram, archive, import]
date: 2025-06-08
description: All posts from my Schriften Telegram channel in one place.
---

````html
NextJs tips 12:

The data that is fetched in the Server component then passed as prop to the Client component, which needs to be serializable by React because it passes a Network boundary!
Objects, arrays, strings, finite numbers,
true, false, and null are serializable
types of data.

Function, RegExp, and Error objects and the undefined value cannot be serialised or restored. (Source).
That means you cannot pass a function as
prop to a Client Component returned by a
Server component.

If you need to pass a component form the
Server to the Client, you can pass a
mapped string then render the component
based on that prop string on the Client

#first
4 April 2024
16:57
Schriften
DB/MySql:
Compound joined condition: joining multiple column together / joining two tables with more than one conditon
17 April 2024
20:51
Schriften
Nextjs tips 16:
Get path name in server nextjs book 16th

Using JavaScript you set a cookie:
“document.cookie = ‘pathname’;
${pathname}; ‘SameSite=Strict’;
‘Secure’”.
Then read the cookie instead of the
header in the Server Compone
21 April 2024
11:24
Schriften
فرانت چپتر 🥕 21.04.2024 11:05:00
Photo
Not included, change data exporting settings to download.
1080×1080, 109.8 KB
🛸 شماره‌ی هشتم از ماهنامه‌ی هویج تایمز منتشر شد!
خلاصه‌ی اخبار دنیای فرانت‌اند در ماهی که گذشت 🪂

⭐ ویژه شماره‌ی فروردین ماه 🔥

فرانت چپتر؛ محیطی صمیمی برای گفت‌وگوی تخصصی
🥕@FrontChapter - #frontChapter
22 April 2024
10:50
Schriften
♚ Erfan Nemati 👨‍💻 ♚ 20.04.2024 21:26:22
https://betterprogramming.pub/10-javascript-promise-challenges-before-you-start-an-interview-c9af8d4144ec
10:50
https://medium.com/frontend-canteen/10-code-challenges-to-master-promise-then-and-promise-catch-3da2bdea1d97
26 April 2024
15:38
Schriften
https://www.youtube.com/watch?v=mpcE5rxgLxM
15:41
In reply to this message
lifting up to the parent layout for preserving different states from different parent-child related routes
15:59
Schriften
NextJs tips 29-30
using server actions and useFormState hooks which gives us the ability to write nodeJs in function and get rid of api call with fetch or axious.
8 May 2024
01:09
Schriften
there is a different between promise constructor and a promise handler. costructor run sync and immediatelythe but the handler run always async.
costrcutor :

const promise1 = new Promise((resolve, reject) => {
console.log(1)
resolve(2)
}
)

this run both log and the 2. the num 2 is now resolved syncorlonsley.

promise handler:

promise1.then(res => {
console.log(res)
})

console.log('end');
;

this .then is run always async. because of that, the response (2 which was already resoved at constructor) logged at the end and after the 'end'.

inside construcor we could have both async and sync actions but the handler runs always async. this prenvents blocking the event loop. the engine when reaches to the .then , it keeps running the codes below it and after finishing all tasks, it display the resolved action.

the whole code:

console.log('start');

const promise1 = new Promise((resolve, reject) => {
console.log(1)
resolve(2)
})

promise1.then(res => {
console.log(res)
})

console.log('end');;
9 May 2024
20:59
Schriften
console.log('start');

const promise1 = new Promise((resolve, reject) => {
console.log(1);
// No resolve or reject called, so promise1 stays pending
});

promise1.then(res => {
console.log(2); // This will not be called because promise1 is still pending
});

console.log('end');

result is start,1,end

num 2 never logged. cause the promise must either resolve or reject and we must write this function explicitly til promise could change its state.
when there is no resolve or reject state, promise will be stay at the peniding state.
when the promise stays at penidng state, the .then func never called.
.then calls only when the promise reloved or rejected, therefor the num 2 log never has been called.
21:07
a Promise constructor is executed synchronously.
22:31
Schriften
In JavaScript EventLoop, there is also the concept of priority.

Tasks with higher priority are called microtasks. Includes: Promise, ObjectObserver, MutationObserver, process.nextTick, async/await .
Tasks with lower priority are called macrotasks. Includes: setTimeout , setInterval and XHR .
10 May 2024
15:45
Schriften
Rendering never happens while the engine executes a task. It doesn’t matter if the task takes a long time. Changes to the DOM are painted only after the task is complete.

Render will be blocked until microtasks are finished so therefore also render will be blocked when you use lots of promises or it has heavy logic inside it
15:56
queueMicrotask is a new browser API which can be used to convert your synchronous code into async.

differnece with setTimeout/setInterval
queueMicrotask will execute microtask in a same queue after all sync microtasks are executed but setTimeout/interval execute tasks in a separate queue (macrotask queue) and because of that these tasks may not execute right after current task completes:

https://freedium.cfd/https://medium.com/@kondareddy_yaramala/understanding-the-power-of-queuemicrotask-webapi-in-javascript-an-in-depth-analysis-eda07eb18009#:~:text=queueMicrotask%20is%20different%20from%20other,after%20the%20current%20task%20completes.
20:48
Schriften
Things like HTTP Requests for AJAX, setTimeout are async (macro or micro) they dont live inside js engine they live in web api env.
when we call them on js, their call back move them in the web api env and they wait until they're done, then based on priorities (macro - micro, etc) return to the queue and their callback will execute
22:46
Schriften
const [number, setNumber] = useState(0);

return (
<>

<h1>{number}</h1>
<button onClick={() => {
setNumber(number + 1);
setNumber(number + 1);
setNumber(number + 1);
}}>+3</button>
</>
)
}

React waits until all code in the event handlers has run before processing your state updates.
this feaure of react lets us update multiple states wihout trigerring too many re renderening. it batches all state updates in one re render. this feat called batching

- Setting state does not change the variable in the existing render, but it requests a new render.
- React processes state updates after event handlers have finished running. This is called batching.
- To update some state multiple times in one event, you can use setNumber(n => n + 1) updater function.

theory:
react first run all the setStates in a handler (add them to the queue one by one) and then after compeleting the handler, it starts re rendering and changing states from reading and executing the queue.

https://react.dev/learn/queueing-a-series-of-state-updates
15 May 2024
01:16
Schriften
regular func can be called before initiallazation cause they will be hoisted and go on top of their scope.
but arrow func since they have to be assigned to a variable, they can not hoist to the top of the scope as a function.
https://www.freecodecamp.org/news/the-difference-between-arrow-functions-and-normal-functions/#:~:text=//%20ReferenceError%3A%20Cannot%20access%20%27printName%27%20before%20initialization
17 May 2024
16:38
Schriften
this is not a property of the function or the object directly; instead, it is a special binding that depends on how the function is invoked.
this in js reffers to the context in which the func (that this is used there) called.
21 May 2024
17:48
Schriften
useState is not async!:
In fact, setCount does its job synchronously. However, the updated value doesn't immediately reflect in the count variable because React batches state updates for performance reasons. This means the count variable isn't updated until the next render
19:15
Schriften
Batching Updates: React batches multiple state updates that occur within the same event loop iteration to improve performance. This means that if you call setCount multiple times within the same function execution, React will only perform one re-render with the final state value.
19:19
js has two phases:
1 - creating executuin context (compiling - hoisting - creating lexical scop env - memory allocation )
2 - execution

the hoisting occurs in the first phase
22 May 2024
00:19
Schriften
how preseving state in react:
React ensures that state updates are preserved between re-renders of the component. Even if the component function is called multiple times (e.g., due to re-renders triggered by parent component updates), the state remains consistent because it's associated with the component instance
16:51
Schriften
difference between OOP and FP
FP emphasizes the use of pure functions, where the output is solely dependent on the input and has no side effects.

in OOP we re using the logic by object inheritance concept. class can accept props of other class.
in FP we re using code by creating higher order func: funcs that receive other funcs as arguments or retun them as result

in FP we could use recursion over itration and make a loop by calling a func instide it instead of useing loop explicitly

OOP uses mutable state within objects.
FP uses immutable state and pure functions.

OOP achieves reusability through inheritance and polymorphism.
FP achieves reusability through function composition and higher-order functions.

polymorphism: it allows an object to be an instance of its parent class. this concept lets us extent a loginc of a class to another classes.
function composition: it allows us to combine functions for creating new function and more complicated logics. in composition, the output of a func could use as in input for antoher function.
17:29
Schriften
when we use composition manually:

const add = x => x + 2;
const multiply = x => x \* 3;

// Function composition manually
const addThenMultiply = x => multiply(add(x));

console.log(addThenMultiply(5));
17:33
when we use higher order functions for function compostion:

const add = x => x + 2;
const multiply = x => x \* 3;

composer = x => firstFunc(secFunct(x));
addThenMultiply = composer(add,nultiply)

console.log(addThenMultiply(5);
17:47
codes in oop is mutable but in fp the best prctice is unmutablity. this is critical to a func to remain pure (result of a func should be separated from the input and input must be isolaited)
18:07
Schriften
Whenever a component's state or props change, React triggers reconciliation.
The Reconciliation Process:

New Virtual DOM Creation: React creates a new virtual DOM reflecting the updated state or props.
Diffing the Virtual DOMs: React compares the previous virtual DOM with the new one to identify the minimal set of changes required.
Updating the Real DOM: Based on the differences, React updates the real DOM efficiently. It might involve:
Modifying existing elements.
Adding new elements.
Removing elements.
23 May 2024
02:02
Schriften
Photo
Not included, change data exporting settings to download.
1280×569, 55.5 KB
how react compiler cashes/memoizes the component and prevent unnessecry re rendering.
by asigning the element to the array of cashable elements
16:54
Schriften
layout in nextJS:
it allows us to build an wrapper around our page, which is stable when routing/navigating. layout is a good idea for developing footer /header of an app and other fixed component.
we could preserve the state that we create in layout in all sub pages/layout.

template in nextJs:
with template is also a wrapper around the page, but it doesnt preserve the state of its page during navigiation/routing, instead it will be re mounted after navigation.
when we want to call an action each time the user enter a page, template is a good idea and we shouldnt use layout for this.
24 May 2024
20:18
Schriften
about && operator:
it returns the first falsy value or the last turthy one:
false && false && asb => false
null && false && undefiend => null
true && true && asb => asb
20:34
Schriften
events in js:
eventPropagation: it has 2 kinds => bubbling - capturing:
bubbling: the event starts to grow from inner element to outer (thats the default behavior of an event in js. to prevent that: e.stopPropation)
capturing: when the event starts from the outher element and keeps moving to the inners. (thats not the default behavior and to make it we can pass the third arugment of enventListener a true value):

.addEventListener('click', function() {
alert("I'm a div");
}, true);

- when the preventDefault is called, the defualtPrevented prop in the element obj is true. e.defaultPrevented = true
  20:44
  e.preventDefault:
  prevent the calling event to have its default actions unless we command them explicitly. when we use it insdie a form submission event, it wont let us submit.
  31 May 2024
  18:02
  Schriften
  about event loop - web apis and
  js is single threaded (it only has one call stack on no more) it can not do taks in parallel. for this reason we use web apis to hadle long running tasks.
  but how:
  some of these web apis allow us to offload long running tasks to the browser and when we call those apis we just initiate the offloading.

whats the task of event loop?
it checks if the call stack is empty. if nothing is running it gets the first available tasks from the tasks queue and gives it to the call stack and so on.

so if there are tasks running in the callstack , async tasks should wait in the queue even they're done. therefor some tasks like setTitmeOut doesnt exacly run on the exact given time.
18:09
web apis are devided to two part:
callback based apis (macro task)
promise based apis (micro task)

event loop in js has antoher responsibility and that is to find and differ micro tasks from macro tasks.
it first gives all the promise based apis (like async fun, fetch, promise mutaionObserver, queueMicroTask...) to the callStack and when the micro tasks qeue is empty, pass only one macro task to the callstack and so on.
18:14
becarefull about infinite microtask loop!
When we do some microtask and inside that taks another micro task, this microtasks could block the enire queue of our macro tasks queue.
3 June 2024
20:24
Schriften
imporve performance:
prevent links to preload
import components which we dont use them on page load dynamically
migrate from sass modules to tailwindCss
prevent unnecessary re rendering by refactoring scrollDirection and scrollPosition feats.
migrate to next14 for imporving server side rendering of components - cashing systen - take advantage of server component in next14
improvement components. server side rendering by separating static parts of the component from dynamic parts.
pass the clinets components as a children to server components for impoving the ssr and use the ssred component as a layout component.
20:38
Photo
Not included, change data exporting settings to download.
1280×710, 70.6 KB
what we do in promise resolve part, we can get it in the .then part of the promise asynchronously.
4 June 2024
14:35
Schriften
SSG: statice site generation:
its a sort of rendering for webPAges. in that the webPage and contents are pre-rendered at build time (no request to server for getting data ) and each time we meet the page, our request gets data from cdn and not server. in this method any change require rebuilding the entire site.
14:37
ISR: Incremental static regeneration
its a combination between ssr and ssg . i this method the webpage is pre-rendered at build time in cdn (like ssg) but there are several methods for revalidating this data on specific time or on demand.
15:56
Schriften
SWR cashing is different from SSG. it cashes on the client side and in localstorage. when we request some data again, it checkes if the cashed data not stale and if its true, it rerurns the cashed data on client side.
7 June 2024
13:58
Schriften
about itrating in js
in js all objects, strings and Sets have a default symbol.iterator which allows them to be iterable.
Symbol.iterator is a built-in symbol that specifies the default iterator for an object

const arr = [1, 2, 3];

// The array has a Symbol.iterator method
const iterator = arr[Symbol.iterator]();

console.log(iterator.next()); // { value: 1, done: false }
14:17
Schriften
Iterable: An object that has a Symbol.iterator method.
Iterator: An object with a next() method that returns { value, done }.
12 June 2024
00:29
Schriften
about WAF - Web aplication firewall:

It typically protects web applications from attacks such as cross-site forgery, cross-site-scripting (XSS), file inclusion, and SQL injection, among others.
While a proxy server protects a client machine’s identity by using an intermediary, a WAF is a type of reverse-proxy, protecting the server from exposure by having clients pass through the WAF before reaching the server.
13 June 2024
16:13
Schriften
Prototype in Js
in js all varialbles could access some methods and props by inheritence. they all have an access to a prop named prototype.
thats why we could use str.splice or array.toString in variables.
also we could add custom methods or props in a func constructor by using prototype:

function Person(first, last, age, eyecolor) {
this.firstName = first;
this.lastName = last;
this.age = age;
this.eyeColor = eyecolor;
}

Person.prototype.name = function() {
return this.firstName + " " + this.lastName;
};
17:29
Schriften
useEffect - useLayoutEffect
both of the are for performing sideEffects. the key difference is the point of performing these sideEffects in component lifeCycle.

useEffect is async and its wait for dom for all mutaion to happend and then wait for all changes to paint in the screen, then it perform the sideEffect and update the ui so user can see the ui updates.

useLayoutEffect is sync. after all dom mutaion is complete, it will block the screen from updating until all sideEffect performed then ui updates and screen will repaint.
useLAyout useCase is when we want to add some loginc to measure layout or add some thing which affects the ui-layout and its better to add it before ui update.

so useEffect is async and it will not block the ui from update.
use layout is sync and it will block ui from update until all effect is perormed in Dom

The effects exsiting in useEffect perform after ui update and in the next rendering cycle
21:10
Schriften
About Rendering proccess:

First js will execute then all styles differences will be calculated
Then reflow (layout) happens:
In this phase the position and the size of all Elements will be calculated with the previous Version.

Then paint happens:
In this phase all the styleing updates will be performed in the elements and pixels will be filled with them.

Then composite happens:
In this phase all of the updates element will be combined together
14 June 2024
13:30
Schriften
useMemo and useCallBack differnece
we use useMemo to memoized a return value and result of a functionaity. useMemo ensures that a re-calclation of an expencive logic only happens when the dependecies changed.
also we use it when the drived state (the state we're passing it to the child component and want to make some calculation on that in a child) only re run when this state changed.
then we use useMemo to prevent recalculation of an expencive logic on every re-render.

const expensiveCalculation = (num) => {
console.log('Calculating...');
return num \* 2;
};

const MyComponent = ({ number }) => {
const memoizedValue = useMemo(() => expensiveCalculation(number), [number]);

return <div>{memoizedValue}</div>;
};

useCallBack:
we use useCallback to memoize a functionality it self and for example pass it to a child component.
useCallback ensures that a function only be called when one of its dependecies changed:

//in a parent component we wrote a memoized onClik func:
const memoizedCallback = useCallback(() => {
doSomething(a, b);
}, [a, b]);

//in a child component we passed this memoized onClick func. it calls only whe the value of this eventHandler changed.
const MyComponent = ({ value }) => {
const handleClick = useCallback(() => {
console.log(value);
}, [value]);

return <button onClick={handleClick}>Click me</button>;
};

#here
14:00
Schriften
Both useMemo and useCallback can be used to optimize performance in a React (or Next.js) application by memoizing values and functions respectively, and their use cases can sometimes overlap
14:04
overusing memoization: Each memoized value or function is stored in memory, which could lead to increased memory usage if overused.
18:14
Schriften
where axactly useMemo and useCallback cashe the value or func:
when in react each eleement or component has a fiber node. fiber node represents each component in react strucutre. when we're passing a value/prop/func to a component , react attaches these props to its related fiber node and preserve it for differeing them from old and new version.
18:18
when a react comp is mounted, react create a fiber node for it. then when the hook is called, react attaches the value or funcs to its fiber.
when the deps are not changed, react use the same value or func in fiber node in re rendering process. when the deps have changed, react re cacualte the funcs or call the func again and update the fiber node
.
18:33
Schriften
On the initial render, React creates the function and stores it in the fiber node.
On subsequent renders, React checks [value]
18:41
overusing memoization leads to:
Increased Garbage Collection Activity.
Memory Leaks
18:49
fiber node are created during the rendering process of components
19:06
Schriften
rendering and mounting process in react:
render phase: call a render method of each component to create a new v-dom
reconcilation: differing this new v-dom to old v-dom
commit phase: applying change from to r-dom and mounting component. useEffect runs in this phase. i.e when the component is mounted
19:13
useEffect runs after comonent is mountned (it runs after commit phase) and when its deps is changed, it triggers a re render.
useMemo or callback runs in render phase and passed to their related to fiber to be stored and differ in next rendering procces.

so useEffect runs after commit phase , useMemo or callback run in render phase.
19 June 2024
19:58
Schriften
useRef:
there are two kind of refs: string and callback.
string refs are direcly set in the dom and callback is set in the func and this func calls on comonent instance or the dom element when they're mounted or updated.
we use refs when we want to access some elment/components props or methods which are not accesible in the components props.
i.e we use refs when we want to access the underlying methods of dom elements or dom it self or instances of them.

function MyComponent() {
const myRef = useRef(null);

const handleClick = () => {
myRef.current.focus();
};

return (
<>
<input type="text" ref={myRef} />
<button onClick={handleClick}>Focus input</button>
</>
);
}
20:23
Schriften
how useRef works:
const ref = useRef(null)

when we call the useRef and asgin it to a var, it return a mutable obj with a prop named current which we can set any value to it.
in the above case, we use the myRef as a refference to a dom element, so the current obj can access the dom element methods.
in this case, current reffers to input element and its method i.e focus.
20:38
Schriften
callBackRefs:
we can wirte a func and pass it as a ref to an element instead of using useRef.
we write a setter func which get an element as an arg and asgin it to variable.
when we pass this setter fun to an element, this element asgin to that variable and then we could use that var inside another func to access its underlying dom methods:

let ref = null;

function setRef(element) {
ref = element;
}
function handle() {
if (ref) {
ref.focus();
}
}

  <input className='bg-v2-text-low_em w-1/2 mr-10' ref={setRef} />
      <ButtonV2 onClick={handle}>ddd</ButtonV2>
20:46
when we could use callbackRefs:
when we want to pass refs to some elements which rendered or destroyed conditionally.
if we make a custom ref in this way we have more control on passing ref to the elements.

triggering actions or sideEffect on component life cycle:
we can make some action this way when component mounted or unmounted. we could pass the seterFunc as a ref only when the component is mounted.

function MyComponent() {
const [showInput, setShowInput] = useState(false);

const handleToggle = () => setShowInput(!showInput);

const setRef = (element) => {
if (element) {
// Element is being mounted
element.focus();
} else {
// Element is being unmounted
console.log('Element is unmounting');
}
};

return (
<>
<button onClick={handleToggle}>Toggle Input</button>
{showInput && <input type="text" ref={setRef} />}
</>
);
}

prevent stale clousure
when some data that must be updated during re-render , remains the same. this could happen when we use useRef. since useRef creates an obj that persist across re-renders. but with custom ref / callback ref we could prevent this , cause the func always calls after re-render and gives us the last instance of the refferencing element.
21:19
Schriften
when useRef called?
useRef call on rendering phase and with every re-render.
on the initial render , it calls in this phase and sets the value to the initial value (null in our case) . then react recocile the dom and v dom and then the commit phase starts. in this phase react commit the changes from v-dom to actual dom. in this phase react asign the ref courrent prop to the refferenced element in dom.

then useRef calls in rendering phase (set to null), it updates the current on commit phase(with element).(this is related to initial render) .
on every re-render the current asigned value persist. so when the useRef calls on rendering phase in every re-render it returns the same current prop.
21:33
commit phase is the last phase of react reconcilation proccess. its unstopable in this phase react runs these the life cycle methods:
componentDidMount, componentDidUpdate, and componentWillUnmount.
assignment of ref cuurent prop occurs right before commonentDidMount /update/ called. didupdate in init render and didUpdate in re-rendering
21:35
useEffect called after componentDidMount and useRef called in rendering phase and it reasigned before componentDidMount
24 June 2024
15:43
Schriften
privatives are passed to variables by their values. but none-primitives (obj, arr, func) are passed to variables by their reference. that the reason why we cant reasign a const variable from an obj to aother but we could mutate its value props.

Reaign a variable means changing its reference. let,var allow us to do that but const doesnt allow us.
27 June 2024
19:19
Schriften
symbol:
they are identifier and unique and unmutable primative in js.
we could use them to create different and unique key for object.

also there are some well-known predefined symbols in js. with them we could change some default behavior of js and create a custom behavior.
ie with symbol.iterator we could make a obj iterable:

const myIterable = { \*[Symbol.iterator]() {
yield 1;
yield 2;
yield 3;
}
};

for (const value of myIterable) {
console.log(value); // 1, 2, 3
}

Symbol.toPrimitive

const obj = {
name: "Alice",
age: 25,
[Symbol.toPrimitive](hint) {
if (hint === "string") {
return `Name: ${this.name}, Age: ${this.age}`;
}
return null;
}
};

we use it to turn an obj to a privmative value
Schriften pinned this message
28 June 2024
21:30
Schriften
react portal
it allows us to render a child outside of the parent/child hierarchy of the dom. this child exists outside of the hierarchy and can be used every where in the dom.
useage:
first create a dom node:

<!-- In your HTML file -->

```html
<body>
  <div id="root"></div>
  <div id="portal-root"></div>
</body>

create the portal component:

// PortalDemo.js
import React from 'react';
import ReactDOM from 'react-dom';

const PortalDemo = ({ children }) => {
const portalRoot = document.getElementById('portal-root');
return ReactDOM.createPortal(children, portalRoot);
};

export default PortalDemo;
1 July 2024
00:42
Schriften
about setImidiate:
in introduce in nodeJs to handle async operation. its not available on browser and istead of it we could use setTimeOut which is a little differnet and percise than setTimeout.

setImidiate allows us to execute a task riight after current eventLoop itration is over.
ie is the fist task that execute right after the current evLoog itration is over.
note that we are taking about nodeJs event loop.

inside those apps which has server-side rendering like nextJs we could use setImidiate because NextJs run in server and client both , so it has access to both node and js apis.
but inside a standart react app we do not have such an access unless we use some polyfill wich gives us a compatible (an alternative) code, so we could use setImidatie in js env too.
00:44
generally polyfills are a piece of code which allow us to use new feats or apis that are not supported in a browser or a native env.
01:39
Schriften
about node and js envs relations:
Node.js provides a runtime environment for executing JavaScript code outside of the browser.

client side js runs by the browser and server-side runs by node.

javascript runs in the context of the Window and the Dom.
every vars defined in the global scope of the js are props of the window
js in browser interacts with DOM . DOM is a representation to the Html elements and it has some props to interact and manipulate the element, like doc.getElementById , appendChild, window.document and so on.
Widow obj represents the browser window and it gives us some method to intract with it, like window.console setTimeOut , scroll., fetch..
01:48
the different between dom and html element:
html is stored at the web server. when we visit a web page we req the server and get the htmls. browser gets the htmls and compile it to what we see. but html is a static structure and cant be changed or manipulate by it self. after html is served and displayed in the browser , browser parses it to an obj named DOM and all element becomes a node in DOM tree. DOM is stored in the browser memory and can be changed and modified by javascript.
02:01
then we can say, client-side js runs on browser through window obj and the serverside js runs in nodeJS env thorigh globalContext.
5 July 2024
00:50
Schriften
about javascript phase:
when html req script and fetch it, the first phase begins:
it is called compiling:
in compling phase js engine create lexical global scope. this env has access to the browser obj window.

#the key envents in this phase:
accessing window obj.

- hoisting var and global variable to the top of the scope
- initialzing them to undefined
- hoisting func declartion and invoking them to create the function scope
- hoisting let and const and other blocked scope
  01:09
  Schriften
  #the key envent in the scond phase : execution phase:
  execuiton happens line by line:
- var and global variable assigned to their related values
- functioons executed
- let will be initialized to the value of that line which declares it
- const must be initialzed to a value on the exact line of creation and it cant be changed.
  01:30
  Schriften
  when we declare a varible without let const and var, it will be hoisted to the global obj or window obj.
  but var is different. when we declare it inside a {} it will be hoisted to global lexical env as a prop of window or global. and when we declare it inside a func scope it will be hoisted on top of that func scope. (not a global variable any more)
  01:46
  Schriften
  compiling phase (hoisting) in js not happens line by line. it happens based on scope priority. it first scans in global scope looking for funcs, var and let or const and hoists them on top of global scope.

then it will scan inside func scopes and do exactly that hoisting inside them.

then it will scan other blocked scope like if , loop or simple {}.
02:04
Schriften
hoisting in js happens based on scope and not line by line:
first everyyhing in global scope:

- funcs
- var
- let const

sec everything in funcs scope:

- funcs and nested funcs and nested funcs in them
- var
- let const

- other blocked scopes like {}, if, loop
  02:18
  the diffenet betweeen this fucking 2 lines :)))

console.log(x);
var x = 2;

// this will log undefined , cause the declaration : var x, will be hoisted and initialized to undefined:
var x = undefinded
console.log(x)
x = 2

console.log(x);
x = 2;

// this will be a refference err x in not defined. cause x = 2 is an asginment and not a declation and we want to access a varibale value before its assignment.

both this assignment happened in globalscope but only first one will be initiallized in the hoisting time . the sec initialliezed when assignment happens.
02:26
the var x = 2 or x = 2
in clinet js , is a window property.

but the var x = 2 in node is not a global propery: global.x = undefined
its a module prop.
x = 2 but is a global prop in node
15:38
Schriften
about lexical env parts:
first: env record:
it stored funcs , parameters, varibale declaraion and asignment and generally handle the bindg between variables and their values inside thee scope.

sec: env outer referrence:
this is a referrence to the outer lexical env (parent) of the current one (child) this part makes a chain of envs that can be goes from down to up when a variable not fount in a scope.
15:55
Schriften
lexical env outer referrence is created in compling time but its useage is at execution time.
it connects child scope to the parent and when a varibale are not hoisted and stored in a env record it goes up and search the parent scope env record.
16:50
Schriften
the compling and creating lexical envs parts and hoisting phase of js happen in the execution context creation.
16:51
js has 2 phase then:
exection context creation (compling)
execuion phase
16:52
scope chaining. its the function of env outer reference

about garbage collection:

Closures Can Prevent Garbage Collection:

If an inner function (closure) maintains a reference to a variable from an outer scope, that variable won't be garbage collected, even if the outer function has finished executing.
js
Copy
Edit
function outer() {
let data = "I am still here"; // Normally, this would be garbage collected

    return function inner() {
        console.log(data); // Closure keeps "data" alive
    };

}

let keepAlive = outer(); // "data" is still in memory because of inner()
keepAlive(); // Logs: "I am still here"
8 July 2024
19:59
Schriften
webP vs svg:
svg format is resolutuon independent and its suitable for logo icons . but webp is good for complex graphics that benefit from rasterization

webp reduce bandwidth and faster load time and has SEO benefits because it affects the load time of sources.

in nextJs the image component autimatically serves the image with the format thats compatible with the user browser. if it supports webP the webP.
svgs are a differenrt format and they're not trnasormed to webP when served. and there is no need for that.
19:59
svgs are vecor format and webP, png, Jpeg are rastor.

rastor made of pixles and each pixle has a unique color and fixed resulition thats why rastor format images are suitable for complex graghics like deaitled image and photos.

vector made of tiny parts difined by mathematical equation this parts can be various shapes, lines text ... . thats why the svgs are suitable for simple graghi. and icon and resulution free
23:28
Schriften
#performance:

decrease FCP load time by preloading FCP contents like banners
decrease initial loading time of sources by turing off the prefetch prop in some unnecessary Link component
layzy loading components to imporve FCP and LCP speed
SSRed component and server cashing for static component by seprating logical component from static ones.
use custom Image component instead of next Image which helped to speed up the build time: next Image has very complex configration of resizing , bluring , format swithcing image and we dont need all of them.
prevent unnecessary rendering because of scroll pos.
change from sass modules to tailwind to prevent scss barrel files to laod on every page.

change method of exporting compoent from default to named for helping tree shaking barreld files:
default exported component could have any name and this way its defficult for tree shaker to detect which part of the code are in used.

help tree shaking process by making a pattern for importing component or libraries and set a 'modularizeImports' field to transform

import { debounce } from 'lodash'

to

import debounce from 'lodash/debounce'

#perf
23:42
turbopach handled the dev env building. nextJs copiler is the build tool for production
9 July 2024
00:01
Schriften
nextJs use swc for compiling and minification on production not babel
00:04
nextJs uses Turbopack for dev build . (next dev) it has a speedy build process and hot module replacement . in production, it uses next compiler (SWC speedy web compiler)
00:04
Hot Module Replacement (HMR): It enables HMR, allowing you to see changes reflected in your browser almost instantly without a full page reload
10 July 2024
11:52
Schriften
call, apply , bind methods:

these methods helping us to manipulate or cusomize a func behavior considering their this binding and the argument we're passing them:

// when we call a func with apply, it recive an arg which specify the this behavior and an array of args we're passing to the func
function greet(name) {
console.log(`Hello, ${name}!`);
}

greet.apply(null, ['Alice']);

call method is exacty like apply but it acecpet infinte value as args:
function greet(name) {
console.log(`Hello, ${name}!`);
}

greet.call(null, 'Bob');

bind method create anouter func with special binding and we could use that func
function greet(name) {
console.log(`Hello, ${name}!`);
}

let greetBob = greet.bind(null, 'Bob');
greetBob();
12 July 2024
20:21
Schriften
line by line executiion in js:
the proccess of executuion in js is line by line . but consider this: when in line by line executing js reaches to a func, it calls it, the func call create aother execution context and push it to a callstack. by calling a func, the process of line by line executing is paused and the new context will executed line by line untl it reaches to another func and so on.
20:22
This nested structure is handled by the call stack, ensuring that the most recent function call is completed first (Last In, First Out - LIFO).
20:33
There are two primary types of execution contexts: the global context and function contexts.
15 July 2024
15:57
Schriften
Git Essentials.pdf
Not included, change data exporting settings to download.
5.8 MB
19 July 2024
02:27
Schriften
AST or Abstract Syntax Tree in js
it created in compile (parsing time). it is a haiarchial structure represnted the source code. it turns souce code to some tokens with all syntax and scope relation of the source code.
useage:
tools like esLint detecting errors warning and best practice with help of AST.
libs like babel use and manimulate ASTs for parsing moders es6+ js to the older versions and make js backward compatible.
the js soruce code must converted at the end to bytecode for execution and this process happens on AST.

one the most important useage of AST is catching syntax errors. when code is parsing the, this steps checks if the syntax rules of js is considered in code or not. this process happens before execution and can prevent run time err.
02:29
const sum = (a, b) => a + b;

Program
└── VariableDeclaration
├── VariableDeclarator
├── Identifier (sum)
└── ArrowFunctionExpression
├── Parameters (a, b)
└── BinaryExpression (+)
├── Identifier (a)
└── Identifier (b)
02:44
Schriften
js parses in browser with JS engine. each browser has its own js engine:

- chrome , edge , opera have V8
- fireFox has spiderMonkey
- safari has JavaScriptCore
- IE and legacy edge have Chakra
  02:50
  then browser handle parsing internally and will catch syntax err before execution.
  but in dev env developers need some comilers to this job before rendering or sending anything to the browser and during development.
  libs like babel, EsPrisma, typescript compiler (tsc)
  20:38
  Schriften
  about eval method in js
  when we want to execute js directly and without compiling and make ast of it, we could use eval method and pass the func as string to it. it executes the source code it self.
  useage of eval:
- executing some codes which are generated at runtime .
- executing scripts which are translated in js only at runtime

Drawbacks of eval

- code injection and not secure
- performance issues because of executing the source code and not the parsed code.

eval is a global func and a prop of window obj.
21:01
Schriften
about garbage collection algorithm
the most common alg in js is mark and sweep.
js marks all global obj and its referrenced objec or func - vars and local vars which are inherently reffrenced by global obj as reachable.
this process coontinues untill all reachable objs are marked. then js scans in memory and find unmarked objs (objc with no refference and useage and then Reclaim the memory occupied by these unmarked objects.
31 July 2024
01:05
Schriften
when useState is called:

- in initial render, it calls and initalaized its state with the given inital value
- in next renders it reads state from internal state.

- when setter func of useState is called the state is updated but not jet diplayed only the old internal states is replaced by the new one . in the next steps the re-render is happened, in this phase useState is called again and read the new state.
- setter is called
- setter update the state with new state (batcing is in this phase
- first update and baching .then() re-render happens and state will be read from useState internall state
  8 August 2024
  17:31
  Schriften
  about loading css and html:
  html and css are loaded in parrarel. but first html is requested and in process of parsing html when browser reaches the style tag or link tag with css a reffrence it starts to req css.

- html parse to DOM and css parse to CSSOM

- css is render blocking . browser wont render and paint html before css is fully loaded because preventing FOUC

- DOM and CSSOM are combined it to render tree

- then painting starts according to this render tree.
  16 August 2024
  00:58
  Schriften
  about throthle and debouche:
  in thorothle we limit a func execution in a period of time. means the func must be executed only once in a specific time:

function throttle(func, delay) {
let lastCall = 0;
return function(...args) {
const now = (new Date).getTime();
if (now - lastCall < delay) {
return;
}
lastCall = now;
return func(...args);
};
}

// Usage Example
window.addEventListener('resize', throttle(function() {
console.log('Resized!');
}, 1000));

debouce ensures the func executed only after the event triggered and the specifice time is passed . means it ensures that a func be executed only when a specific time is passed from triggering an event.

function debounce(func, delay) {
let timeoutId;
return function(...args) {
clearTimeout(timeoutId);
timeoutId = setTimeout(() => {
func(...args);
}, delay);
};
}

// Usage Example
const searchInput = document.getElementById('searchInput');
searchInput.addEventListener('input', debounce(function(event) {
console.log('Search Query:', event.target.value);
}, 300));
13:37
Schriften
appRouter and page router:
pages router was the inital routing sysyem of next, you define your pages inside pages dir it was much simpler.
appRouter is the new v of routing. it lets us to create nested Route with different layout/template which can rendered totally on server(layout) and not re render on route changing. it unlucks server component also.
14:23
Schriften
another feat of next app router is streaming. it alows the component not only rendered on server , also it send these parts chunk by chunk to browser and will not wait for whole page to be fully rendered anymore.
24 August 2024
00:53
Schriften
about shadow dom
with shadow dom we could create another dom inside the dom to encapsulate the shadow from real. we do that when we want to make sure that a custom component inisde the shadow dom wont be affected by js logics or css styling in outer dom dom and also the shadow dom wont affect them.

<body>
    <greeting-message></greeting-message>

    <script>
        // Define a new class for the custom element
        class GreetingMessage extends HTMLElement {
            constructor() {
                super(); // Always call super() first in the constructor.
                const shadow = this.attachShadow({ mode: 'open' });
                const wrapper = document.createElement('div');
                wrapper.textContent = 'Hello, world!';

                // Add some styles to the shadow DOM
                const style = document.createElement('style');
                style.textContent = `
                    div {
                        color: white;
                        background-color: black;
                        padding: 10px;
                        border-radius: 5px;
                    }
                `;
                shadow.appendChild(style);
                shadow.appendChild(wrapper);
            }
        }
        customElements.define('greeting-message', GreetingMessage);
    </script>

25 August 2024
00:02
Schriften
shallow copy and deep copy
when we shallow copy an obj, this process copy all the top level props (means non-nested props like obj or arr) and when in that cpied obj exists some nested props , they will be shared between to variabale.

- shallow copy , copy the top level prop with (primary values) and only copy the refferences of nested props.
- deep copy, copy all of the obj / arr props.

shallow copy:

const original = { prop: 123, nested: { innerProp: 456 } };
const shallowCopy = Object.assign({}, original);

shallowCopy.prop = 789;
shallowCopy.nested.innerProp = 999;

console.log(original.prop); // Outputs: 123 (different value, since primitive values are copied)
console.log(original.nested.innerProp); // Outputs: 999 (same object, so nested object is shared)

const original = { prop: 123, nested: { innerProp: 456 } };
const shallowCopy = { ...original };

shallowCopy.prop = 789;
shallowCopy.nested.innerProp = 999;

console.log(original.prop); // Outputs: 123 (primitive value is copied)
console.log(original.nested.innerProp); // Outputs: 999 (nested object is shared)
28 August 2024
09:57
Schriften
about new Map:
its for creating obj. it allows us to create key - value pairs llike regular obj with this differences:

- keys can be anything even func
- it preseve the exact order of props when mapping through the props
- its faster when it comes to removal and adding prop:

const map = new Map();
map.set('name', 'John'); // String as a key
map.set(1, 'one'); // Number as a key
map.set(true, 'yes'); // Boolean as a key

console.log(map.get('name'));

//map through the Map obj:
// Using for...of
for (const [key, value] of map) {
console.log(key, value);
}

// Using forEach
map.forEach((value, key) => {
console.log(key, value);
});
11:11
Schriften
about new WeakMap:
its like Map but only accept obj as key and it holds a weak refference to that obj i.e when there is no outer reffernece to that obj, the related prop of the weak map obj, will be garbage collected (removed) automatically.

we could use weakmap to hold private data or to prevent memory leaks by using eventHandlers.
weak map is not iterable.
example of uing Weakmap in handling event:

// Create a WeakMap to store click counts associated with each element
const clickCounts = new WeakMap();

// Function to handle click events
function handleClick(event) {
const element = event.currentTarget;

// Get the current count or initialize it to 0 if it's the first click
let count = clickCounts.get(element) || 0;
count += 1;

// Update the click count in the WeakMap
clickCounts.set(element, count);

console.log(`Element clicked ${count} times`);
}

// Create some buttons to demonstrate
const button1 = document.createElement('button');
button1.textContent = 'Button 1';
button1.style.margin = '5px';

const button2 = document.createElement('button');
button2.textContent = 'Button 2';
button2.style.margin = '5px';

// Attach event listeners to the buttons
button1.addEventListener('click', handleClick);
button2.addEventListener('click', handleClick);

// Add the buttons to the document body
document.body.appendChild(button1);
document.body.appendChild(button2);

// Example: Removing button1 from the DOM after some time
setTimeout(() => {
document.body.removeChild(button1);
console.log('Button 1 removed from the DOM');
}, 5000); // Remove after 5 seconds

when the btn is removed from dom, the handler inside the handleClick func can not call anymore and the clickCount variable has no other refference.
31 August 2024
20:05
Schriften
React_18_Design_Patterns_and_Best_Practices_Design,\_build,\_and_deploy.pdf
Not included, change data exporting settings to download.
12.7 MB
#book
2 September 2024
18:21
Schriften
useOnNavigationBAckV2 - solved the modalHash replaceing with query issue:

import { useGetAsPath } from '@/hooks/useGetAsPath';
import { SimpleFunction } from '@/types';
import { useParams, useRouter } from 'next/navigation';
import { useEffect } from 'react';

const currentModeRef: {
modalId: string | null;
state: 'opening' | 'closing' | 'idle';
onCloseCallback: SimpleFunction | null;
} = { state: 'idle', modalId: null, onCloseCallback: null };

interface Props {
onClose?: SimpleFunction;
}

const updateModalState = () => {
if (currentModeRef.state === 'opening' && currentModeRef.modalId === window.location.hash) {
currentModeRef.state = 'idle';
currentModeRef.modalId = null;
return;
}
if (currentModeRef.state === 'closing' && currentModeRef.modalId !== window.location.hash) {
currentModeRef.state = 'idle';
currentModeRef.onCloseCallback?.();
currentModeRef.onCloseCallback = null;
currentModeRef.modalId = null;
return;
}
if (currentModeRef.state === 'idle' && !window.location.hash) {
currentModeRef.onCloseCallback?.();
currentModeRef.onCloseCallback = null;
currentModeRef.modalId = null;
}
};

export function useOnNativeBackV2({ onClose }: Props = {}) {
const router = useRouter();
const path = useGetAsPath();

const addHashToUrl = (modalHashId: `#${string}`) => {
const currentUrl = new URL(window.location.href);
currentUrl.hash = modalHashId;
return currentUrl.toString();
};

return {
openModal: (modalHashId: `#${string}`) => {
currentModeRef.onCloseCallback = onClose || null;
if (currentModeRef.state === 'idle' && currentModeRef.modalId !== modalHashId) {
currentModeRef.state = 'opening';
currentModeRef.modalId = modalHashId;
const fullUrl = addHashToUrl(modalHashId);
window.history.replaceState(null, '', fullUrl); // Use pushState to add a new entry in the history
}
},
closeModal: (modalHashId: `#${string}`, afterCloseCallBack?: SimpleFunction) => {
if (currentModeRef.state === 'opening') {
if (window.location.hash === modalHashId) {
if (afterCloseCallBack) {
currentModeRef.onCloseCallback = afterCloseCallBack;
}
currentModeRef.state = 'closing';
currentModeRef.modalId = modalHashId;
router.replace(path);
currentModeRef.onCloseCallback?.();
}
}
}
};
}

export const usePopStateListenerV2 = () => {
const params = useParams();
useEffect(() => {
updateModalState();
// eslint-disable-next-line react-hooks/exhaustive-deps
}, [params]);
};
19:05
Schriften
React is split into two packages:
• react: Implements the core features of the library
• react-dom: Contains all the browser-related features
19:29
Schriften
we can extend interface with type and vice versa:

interface IWork {
company: string
position: string
}
type TPerson = IWork & {
name: string
age: number
}
20:54
Schriften
In reply to this message
The react-dom package provides DOM-specific methods that can be used at the top level of your app and as an escape hatch to get outside the React model if you need to. the important methods of react-dom:
ReactDOM.render() replaces the child of the given container if any. It uses a highly efficient diff algorithm and can modify any subtree of the DOM.

- render(): This is one of the most important methods of ReactDOM. This function is used to render a single React Component or several Components wrapped together in a Component or a div element.

- findDOMNode(): This function is generally used to get the DOM node where a particular React component was rendered. This method is very less used like the following can be done by adding a ref attribute to each component itself.

- unmountComponentAtNode(): This function is used to unmount or remove the React Component that was rendered to a particular container.

- hydrate(): This method is equivalent to the render() method but is implemented while using server-side rendering.

- createPortal(): It allow us to render a component into a DOM node that resides outside the current DOM hierarchy of the parent component.

React

- Whenever we use component, classes, elements, etc. We’re using React
  21:00
  reactDom.render is deprecated and replaced with reactDom.createRoot((document.getElementById('root')).render(<App/>)
  because of these changes we could use new feats of react 18.
  ReactDOM.hydrate(): In React 18, hydrate has been replaced by hydrateRoot(), which aligns with the createRoot() API.
  3 September 2024
  00:45
  Schriften
  the most important feat of react 18 is the Concurrent Rendering i think. it allows react to differ urgent and non-urgent task and allows browser to be interactive to user action event when some tasks are in process. this means rendering after setting a state wont block the thread and user is still able to click some btn and trigger an event.
  to reach this we could use some hook like useTransition:

import React, { useState, useTransition } from 'react';
import { createRoot } from 'react-dom/client';

// A component that generates a large list of numbers
function SlowList({ count }) {
const items = [];
for (let i = 0; i < count; i++) {
items.push(<li key={i}>Item {i + 1}</li>);
}
return <ul>{items}</ul>;
}

function App() {
const [count, setCount] = useState(0); // Urgent state
const [listCount, setListCount] = useState(0); // Non-urgent state

// Hook to manage transitions (non-urgent updates)
const [isPending, startTransition] = useTransition();

// Handle button click - this is an urgent update
const handleButtonClick = () => {
setCount(count + 1); // Urgent update
};

// Handle list rendering - this is a non-urgent update
const handleSlowUpdate = () => {
startTransition(() => {
setListCount(5000); // Non-urgent update, can be deferred
});
};

return (

<div>
<h1>Concurrent Rendering Example</h1>
<button onClick={handleButtonClick}>
Increment Count (Urgent): {count}
</button>
<br />
<button onClick={handleSlowUpdate} disabled={isPending}>
Render Large List (Non-Urgent)
</button>
{isPending && <p>Loading...</p>}
<SlowList count={listCount} />
</div>
);
}

// Render the App using createRoot (Concurrent mode enabled)
const root = createRoot(document.getElementById('root'));
root.render(<App />);
4 September 2024
22:43
Schriften
enum in ts:
we can use them for keeping set of primative values:

export enum Status {
Idle = 'IDLE',
Loading = 'LOADING',
Success = 'SUCCESS',
Error = 'ERROR',
}

const [status, setStatus] = useState<Status>(Status.Idle);
5 September 2024
01:09
Schriften
namespace:
we use them for grouping set of data togather and use them whrere needed:

namespace MyNamespace {
export const greeting = 'Hello, World!';

export function sayHello() {
console.log(greeting);
}

export interface User {
name: string;
age: number;
}
}

// Using the namespace
MyNamespace.sayHello();
14:48
Schriften
Adjacent JSX elements must be wrapped in an enclosing tag.
we must to wrap the multiple elements inside an element or fragment, cause jsx transpile to Js func and we can not retrun two funcs in js.
23:22
Schriften
about currying:
when a func accept to params, we can convert it to accept only one param at the time and returning anohter func with the other param.
we could use this mehtod when we want to store a value and use it in different places. (when the first func called, the value is stored.)

function name(x) {
return (y) => x + y
}
const b = name(1)
b(2)
///log 3
//this method called currying
//antoher way of calling this func:
name(1)(2)
6 September 2024
01:54
Schriften
HOCs are functions that take a component as input and return an enhanced component as out-
put

const withClassName = Component => props => (
<Component {...props} className="my-class" />
)
20:37
Schriften
unctrolled and controlled comps (in form handling)
when we let dom to handle value of an input and we just handle the changing of input to get the value in give it to submit. this method of handling is uncontrlled component, cause we have no controll on manging the value:

const [values, setValues] = useState({ firstName: '', lastName: '' })
const handleChange = ({ target: { name, value } }) => {
setValues({
...values,
[name]: value
})
}

return (

  <form onSubmit={handleSubmit}>
    <input
      type="text"
      name="firstName"
      onChange={handleChange}
/> <input
      type="text"
      name="lastName"
      onChange={handleChange}
/>
    <button>Submit</button>
  </form>
)
20:40
when we manage and controll the form value by using the state. in this mehtod we must expecitly add a value prop to the input element and set it to its related state:

const [values, setValues] = useState({ firstName: 'Carlos', lastName:
'Santana' })

const handleChange = ({ target: { name, value } }) => {
setValues({
[name]: value
})
}
const handleSubmit = (e) => {
e.preventDefault()
console.log(`${values.firstName} ${values.lastName}`)
}

return (

  <form onSubmit={handleSubmit}>
    <input
        type="text"
        name="firstName"
        value={values.firstName}
        onChange={handleChange}
/> <input
        type="text"
        name="lastName"
        value={values.lastName}
        onChange={handleChange}
/>
22:05
Schriften
event handling and synthetic event in react:
events work differenet on various browser and react get and abstract these events and ease the developers event handling. because of that we could write event handlers that are unaware of the browser target.
to do this react introduced the synthetic event. an obj that wrap the orginal rvent provided by browser with same props.

means in react we dont have to use the window prrop eventListener. cause the events are catched in react and we could get them as a syntheticEvents prop.

const handleClick = (syntheticEvent) => {
//nativeEvent is the browser native event and we could even reach it in react!
console.log(syntheticEvent.nativeEvent instanceof MouseEvent)
console.log(syntheticEvent.type === 'click')
//...
}
8 September 2024
19:32
Schriften
event pooling in react:
in plain js when we create an eventHandler and use it for a btn onclick for example, this handler create a new event obj every time the btn clicked and this is heavy and talke a lot memory. so react create an cross-browser obj named synethetic event which wrappes around the event obj. when we create a handler and pass the event (syntetich event in here) to it, it calls and triggers the event. after the event finishes running it clears all the props of this obj to null and make it reusable for the next time.
to prevent this event pooling we could use event.persist()

import React from 'react';

function EventPoolingExample() {
const handleClick = (event) => {
//when we uncommet this we could persist the event obj
// event.persist()
// Here, React will pool the event after this function runs
console.log(event.type); // Works here
setTimeout(() => {
// The event properties will be cleared before this runs
console.log(event.type); // Will likely be `null` or cause an error
}, 1000);
};

return <button onClick={handleClick}>Click Me</button>;
}

export default EventPoolingExample;

Event pooling has been deprecated in React 17+
20:16
Schriften
event delegation in react
react does not attach a listener in to each element and the func handlers will not directly call in react. instead react uses a top level event listener which has been set on the top of the project (document or root)

import React from 'react';

function List() {
const handleItemClick = (event) => {
alert(`Item clicked: ${event.target.textContent}`);
};

return (

<ul onClick={handleItemClick}>
<li>Item 1</li>
<li>Item 2</li>
<li>Item 3</li>
</ul>
);
}

export default Listt

in this case when we click on one of the li, this click event bubble up to the dom, to that top level listenrer (the handler is not called yet). in this point react wrapps this event iside the ssynthetd event and starts to find the related elment then it calls its handler whith the correct syntetich event prop
9 September 2024
23:43
Schriften
an important difference between synthetic and native events is the performance.
native events might be set separatly in each element with a handler and these events are unique objs an have their specified space in memory and remains until garbage collection. instead
Synthetic Events: Designed to optimize performance through pooling, reducing the number of objects created and saved in memory.
18 September 2024
00:08
Schriften
Key Functions of a Module Bundler in React
combining multiple files
reducing browsers req by combinng modules/js or image or css resouces in to one bundle. code spliting and lazyLoading , tree shaking the dead code (when a huge lib imported but only one method used), transpliling, HMR (hot module replacement)

popular react module bundlers:
webpack, parcel, vite , rollUp
19 September 2024
00:50
Schriften
how webpack modulrize css:
by default js has no idea about css codes but webpack turn(bundle) css to js module and inject it in to js module system. it does that helping loaders.
the most imprtant loader is:
css-loader: without it react doestnt understand import styles.css file in a component. css-loader tranform the css content (@import to require) to js module and export it as string and inject it to the dom.

style-loader: this loader inject css to the dom via a <style> tag. its useful for dev mode because giving the reatime updating css changes but not recommended in production mode because of making bundle larger and preventthe caching css.

mini-css-extract-plugin: this loader replaced with style-loader(production) and extarcats css from js in to separate .css file. this is important for production because it allows browser to load css in parrallel with js and cache it.

in style-loader, css is embeded in to js and that make a huge bundle but because of this embeding it allows us a real-time css updates.

so:

- the css-loader is for bundling css file in to js
- style-loader and mini-css-extract-plugin is for injecting css file to the dom. one in <style> tag and one in separate .css file.
  00:55
  in nextJS there is no need for webpack configurations because its already done and next use the webpack and the mentioned loaders undert the hood.
  20 September 2024
  13:23
  Schriften
  about vite the new module bundler:
  an important difference is the way of handling modules on dev. older bundler like webpack must bundle and build the whole app before serving it on server on dev env. but vite deosnt bundle anything on dev, it serves files as es moudle and when something changes it update and reload only that file and its deps making HMR faster.
  on production vite use Rollup module bundler under the hood.
  7 October 2024
  21:03
  Schriften
  concurent mode in react
  rendering in tradtional react was sync and happend in a single theread but in react 18 rendering is splitted to smaller unit of work and each part can process in parallel.
  React can prioritize certain tasks, such
  as updating the user interface, while still allowing other tasks to run in the background, such as
  handling user input or fetching data.

#there
9 October 2024
18:53
Schriften
Rendering and hydration in react 18
rendering is the proccess of converting react compoennt to dom element and displaying it on screeen.

const root = ReactDOM.createRoot(document.getElementById('root'),)
root.render(<App />)

hydration is the attaching event listenders and handlers to the already rendered from server in client and making the ssred comp interactive.

const root = createRoot(document.getElementById('root'))
hydrateRoot(document.getElementById('root'), <App />)
10 October 2024
00:29
Schriften
renderToPipeableStream
its another ss method in react 18. instead if rendering all the html content and then send it to the client, this method allows us to render content part by part and send it part by part to the client.
his means the browser can start displaying the page's content bit by bit, improving the user experience.
Once the full HTML is rendered and sent, React can take over on the client side to "hydrate" the app, attaching event listeners and making the page interactive.

import { renderToPipeableStream } from 'react-dom/server';
import App from './App'; // Your main React component

const server = require('http').createServer((req, res) => {
// Start streaming the React app as HTML
const stream = renderToPipeableStream(<App />, {
onShellReady() {
// Pipe the stream to the response (send HTML to the browser)
stream.pipe(res);
},
onError(err) {
console.error(err);
}
});
});

server.listen(3000);
00:59
Schriften
useDeferredValue: It doesn't explicitly limit the rate at which updates happen. Instead, it defers the value update until the UI has finished rendering more critical updates. It allows React to prioritize rendering the essential parts of the UI first, while deferring the less urgent updates, making the UI more responsive.

import { useState, useTransition, useDeferredValue } from 'react';

function SearchComponent({ items }) {
const [query, setQuery] = useState('');
const [isPending, startTransition] = useTransition(); // useTransition hook
const deferredQuery = useDeferredValue(query); // useDeferredValue hook

// Handle input changes using a transition to avoid blocking UI
const handleInputChange = (e) => {
const newValue = e.target.value;
startTransition(() => { // Marking the update as low priority
setQuery(newValue);
});
};

// Filtering the items using the deferred value to make sure the UI remains responsive
const filteredItems = items.filter(item => item.includes(deferredQuery));

return (

<div>
<input
        value={query}
        onChange={handleInputChange}
        placeholder="Search..."
      />

      {/* Show loading state when the transition is pending */}
      {isPending ? <p>Loading...</p> : null}

      <ul>
        {filteredItems.map(item => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </div>

);
}
01:09
useInsertionEffect is run right after the element is inserted to a dom its like useEffect and layoutEffect but it runs beofre them:
1- run useInsertionEffect - called before any dom updates after JSX transpilation
2- run useLayoutEffect - called after dom updated and before paitned
3- run useEffect - called async after dom updated and painted
28 October 2024
18:57
Schriften
about concurrent rendering:
The fact that a typical state update blocks the main task is what Concurrent Rendering aims to combat. With it, we can explicitly mark some state updates and the re-rendering caused by them as "non-critical"

As a result, React will calculate these updates in the "background" instead of blocking the main task. If something "critical" happens (i.e., a normal state update), React will pause its "background" rendering, execute the critical update, and then either return to the previous task or abandon it completely and start a new one.
19:03
useTransition , deferredValue, or suspence is two other ways of concurret rendering

export default function App() {
const [tab, setTab] = useState('issues');

// add the useTransition hook
const [isPending, startTransition] = useTransition();

return (

<div className="container">
<div className="tabs">
...
<TabButton
// indicate that the content is loading
isLoading={isPending}
onClick={() => {
// call setTab inside a function
// that is passed to startTransition
startTransition(() => {
setTab('projects');
});
}}
name="Projects"
/>
...
</div>
...
</div>
);
}
29 October 2024
23:34
Schriften
about useTransition and its downSilded
https://www.developerway.com/posts/use-transition
30 October 2024
21:26
Schriften
about throttle in js and react:
simple explaination is: throttle specified how many time can a func be called in a specific time. i,e when we set a dely to 1 sec, the func can be called only one sec after its last call no matter how many time we trigger it.
in js:

function throttle(cb, delay) {
let lastCall = 0;

return function (...args) {
const now = new Date().getTime();
if (now - lastCall >= delay) {
lastCall = now;
return cb(...args);
}
return null;
};
}

throttle in react as a hook:

function useThrottle(cb, delay) {
const lastCall = useRef(0);
// also you can create another ref and pass the simple func wuth args to the current method of i
// instead of useCallBack
const throttledCB = useCallback(
(...args) => {
const now = new Date().getTime();

      if (now - lastCall >= delay) {
        lastCall.current = now;
        return cb(...args);
      }
      return null;
    },
    [cb, delay]

);

return throttledCB;
}
31 October 2024
16:50
Schriften
about debounce:
debounce lets us to call a func after user stops an action and the time has reached to the sepecified dely.
in throtteling the time is fixed we set a delay and the func will be called after the delay is over no matter if the user is still in action or not. but in debouncing, the time is reset after each user actions and the func never be called unless user stops trigerring the action and the time reached to delay.

deboincing in JS

function debounce(cb, delay) {
let timer;
return function (...args) {
clearTimeout(timer);
timer = setTimeout(() => {
cb(...args);
}, delay);
};
}

debouncing in react:

function useDebounce(cb, delay) {
const timeoutRef = useRef(0);
const debouncedFunc = useCallback(
(...args) => {
if (timeoutRef.current) {
clearTimeout(timeoutRef.current);
}

      timeoutRef.current = setTimeout(() => {
        cb(...args);
      }, [delay]);
    },
    [delay, cb]

);
return debouncedFunc;
}
16:54
👆 throttle vs debounce for last fuckin time 👆
1 November 2024
01:43
Schriften
do performant animgation.
avoid using css pops in animating which trigger painitng or layout. we can experiment that by chrome dev tools. performance tap, record and see the rendering percentage and animation frame.
we must always use transform or opacity related props. something other than them should use very carrefully because of paint and layout triggering.
01:43
These four steps are known as the browser's rendering pipeline.
1- Style: Calculate the styles that apply to the elements.
2- Layout: Generate the geometry and position for each element.
3- Paint: Fill out the pixels for each element into layers.
4- Composite: Draw the layers to the screen.
01:58
CSS vs JavaScript performance
You might wonder: is it better from a performance perspective to use CSS or JavaScript for animations?

CSS-based animations, and Web Animations (in the browsers that support the API), are typically handled on a thread known as the compositor thread. This is different from the browser's main thread, where styling, layout, painting, and JavaScript are executed. This means that if the browser is running some expensive tasks on the main thread, these animations can keep going without being interrupted.

As explained in this article, other changes to transforms and opacity can, in many cases, also be handled by the compositor thread.

If any animation triggers paint, layout, or both, the main thread will be required to do work. This is true for both CSS and JavaScript animations

https://web.dev/articles/animations-overview
02:01
transorm and opacity animations affect composite step and take less works agains width or heitg or top or bottom which are a layout related props
20:04
Schriften
about will-change in css:

- this property can be used in situations when an animated element will be repated constantly or regulary.
- with setting that we're teling the browser that the element will change soon so it keeps the optimization of the animation for next time.

in fact,

- by default browser makes for transform and opacity a new layer and remove it automatically by ending the process.
- with will-change , after an animation accures, browser create and persist a new rendering layer.
- thats why we should use thi prop carefully. it creats and keep new layer for each element with this prop
- creating too many layers can cause performace issues.
- with will-change we could persist the animation-transtion layer
  3 November 2024
  23:05
  Schriften
  About react router

BrowserRouter sets up the application's navigation context, while Route defines individual routes, and Switch ensures only one route is rendered at a time
23:22
Schriften
About routGuard

// In a component
import { Route, Redirect } from 'react-router-dom';

function PrivateRoute({ children, isAuthenticated }) {
return (
<Route
render={({ location }) =>
isAuthenticated ? (
children
) : (
<Redirect to={{ pathname: '/login', state: { from: location } }} />
)
}
/>
);
}
23:24
To handle 404 err in react, we add a Route comp without any path prop and a component prop with 404 content.

import { Route, Switch } from 'react-router-dom';

function

NotFound() {
return <h2>404 - Not Found</h2>;
}

function App() {
return (
<Switch>
{/_ Other routes _/}
<Route component={NotFound} />
</Switch>
);
}
4 November 2024
01:17
Schriften
about loader in react router 6.4
it allows us to fetch and load data without using useEffect. we create a loaderData func and pass it to the Route comp of the related page and then inside the page comp we use the useLoaderData to receive the fetched data. with useNavigation hook we can get a pending state before getting the res from useLoader data:

page 218 / 189 of React_18 design pattern
5 November 2024
00:18
Schriften
about react router 6.4 feats:

- client side routing: instead of requesting the server to get a new document and load assets - css on every route navigations, it allows us to update url without sending another req for another document.
- nested routes with createBrowserRouter and createRoutesFromElements:

createBrowserRouter(
createRoutesFromElements(
<Route path="/" element={<Root />}>
<Route path="contact" element={<Contact />} />
<Route
path="dashboard"
element={<Dashboard />}
loader={({ request }) =>
fetch("/api/dashboard.json", {
signal: request.signal,
})
}
/>
<Route element={<AuthLayout />}>
<Route
path="login"
element={<Login />}
loader={redirectIfUser}
/>
<Route path="logout" action={logoutUser} />
</Route>
</Route>
)
);

- getting dynamic parameter in routhe with useMatch
- NavLink allows us to create a navigaton bar and differ the acitve inactive routes:

<NavLink
style={({ isActive, isPending }) => {
return {
color: isActive ? "red" : "inherit",
};
}}
className={({ isActive, isPending }) => {
return isActive ? "active" : isPending ? "pending" : "";
}}
/>

- data fetching with using loader prop inside the Route comp and get the fetched data inside the page comp with useLoaderData
- pending status with useNavigation when using the loader in the way that the data for the next page will loaded before the new page is rendered.

function Root() {
const navigation = useNavigation();
return (

<div>
{navigation.state === "loading" && <GlobalSpinner />}
<FakeSidebar />
<Outlet />
<FakeFooter />
</div>
);
}

- pending status with defer method - Suspense and the Await comp inside it in the way that loading data for the new page is after entering inside it:

<Route
path="issue/:issueId"
element={<Issue />}
loader={async ({ params }) => {
// these are promises, but _not_ awaited
const comments = fake.getIssueComments(params.issueId);
const history = fake.getIssueHistory(params.issueId);
// the issue, however, _is_ awaited
const issue = await fake.getIssue(params.issueId);

    // defer enables suspense for the un-awaited promises
    return defer({ issue, comments, history });

}}
/>;

function Issue() {
const { issue, history, comments } = useLoaderData();
return (

<div>
<IssueDescription issue={issue} />

      {/* Suspense provides the placeholder fallback */}
      <Suspense fallback={<IssueHistorySkeleton />}>
        {/* Await manages the deferred data (promise) */}
        <Await resolve={history}>
          {/* this calls back when the data is resolved */}
          {(resolvedHistory) => (
            <IssueHistory history={resolvedHistory} />
          )}
        </Await>
      </Suspense>

.
.
.

- race condtion handlng: when a async taske starts before another new task but resolve after that. this results the ui shows the wrong state.
  react router wont let this issue occurs. it cancel the async task after starting new task which changes the state:

?q=ry |---------------|
^ commit wrong state (which can be canceled by react router system)
?q=ryan |--------|
^ lose correct state

- err handling: react handles err in rendering, laoding data. but not err realted to hooks or event handlers. react handle the two mentioned err with errorElement prop inside the Route comp. if the comp doesnt have one, the err bubble up to first parent route with that prop.
- scroll preserving with ScrollRestoration comp
- get loaction props of the winodw with useLocation. also we can add some state to link with specifice path and get that state with this hook:
`
function App() {
const navigate = useNavigate();
00:18
return (
<>
<Link to="/home" state={{ someValue: "example" }}>
Go to home page with state
</Link>
<button
onClick={() =>
navigate("/home", {
state: { someValue: "example" },
})
}
>
Go to home page with state
</button>
</>
);
}

`
6 November 2024
18:08
Schriften
{
var name = "mohsen";
}
console.log(name);

var name = "test"

const cars = ["bmw", "mercedes"];
cars[0] = "ford"

const name = "fabod";
name[0] = "\_"

promise(() => {
settimeout(() => {
console.log("s1");
}, 0)
});

settimeout(() => {
console.log("s2");
}, 0)

promise(() => {
console.log("p1");
});

farbod deylami, 5:35 PM

<div>
<button />
</div>

snapp interview
13 November 2024
13:03
Schriften
https://codesandbox.io/p/sandbox/interview-forked-m2x7y6?file=%2Fsrc%2FApp.tsx%3A1%2C1-78%2C1
timer challange

import React, { useState, useEffect, useRef } from "react";

function Timer() {
const time = useRef(50);
var [counter, setCounter] = useState(0);
const [laps, setLaps] = useState([]);

const timer = useRef();

useEffect(function () {
let sec = counter;
// Start the timer automatically on mount (not ideal)
timer.current = setInterval(function () {
sec += 1;
setCounter(sec); // Wrong way of managing state
}, 1000);

    return function () {
      clearInterval(timer.current); // Not properly clearing the interval
    };

}, []);

function startTimer() {
if (!timer.current) {
let sec = counter;
timer.current = setInterval(function () {
sec += 1;
setCounter(sec);
}, 1000);
}
}

function stopTimer() {
clearInterval(timer.current); // This won't stop the timer correctly
timer.current = null;
}

function resetTimer() {
time.current = 0;
setCounter(0);
setLaps([]); // This doesn't trigger a re-render for laps
stopTimer();
}

function addLap() {
setLaps((prev) => [...prev, counter]);
}

function getTime(counter) {
const hrs = Math.floor(counter / 3600);
const mins = Math.floor((counter % 3600) / 60);
const secs = counter % 60;

    const formattedHrs = String(hrs).padStart(2, "0");
    const formattedMins = String(mins).padStart(2, "0");
    const formattedSecs = String(secs).padStart(2, "0");

    return `${formattedHrs}:${formattedMins}:${formattedSecs}`;

}

return (

<div>
<h1>Timer: {getTime(counter)} seconds</h1>
<button onClick={startTimer}>Start</button>
<button onClick={stopTimer}>Stop</button>
<button onClick={resetTimer}>Reset</button>
<button onClick={addLap}>Lap</button>
<div>
{laps?.map((lap) => (
<div>{lap}</div>
))}
</div>
</div>
);
}

export default Timer;
18 November 2024
23:16
Schriften
react security in xss attack (script injecting)
in react we use curly braces to add js in to the markup. injected script behaves like simple string in jsx before rendering in dom:

const userInput = "<script>alert('XSS')</script>";
// this injected script wont execute in react and jsx turns it to a string and send it to the dom.
return <div>{userInput}</div>;
23:25
about dangerouslySetInnerHTML
when we use this prop, react wont scape from executing script and an xss attack is possible by using it. this prop, direcly inject html to the dom and it might contains some malicous script in it.

return <div dangerouslySetInnerHTML={{ __html: comment }}></div>;

therefor when we must use it, its safer to sanitize the prop value. sanitizing the content could remove all possible dangerous code like script, onError, iFrame ...
we could do that my libs like domPurify or sanitize-html.
19 November 2024
00:30
Schriften
about CSRF:
Cross-Site Request Forgery.
tricks an authenticated user into unknowingly submitting a request to a web application they are logged into, but from a different origin (e.g., a malicious website). This allows the attacker to perform actions on behalf of the user, such as:

- Changing account settings
- Transferring funds
- Deleting data

how to prevent:
same origin policy. every origin is defined by 3 methods:

- Scheme (e.g., http or https)
- Host (e.g., example.com)
- Port (e.g., 80, 443)
  urls have same origing if all these 3 are the same. same origin policy prevent the attecker req to get and read res from the attecked site.

another way of prevent CSRF attack is setting a CSRF token in back and hiding it in the forms as input and send it again by submission. the server can check if both sent and received tokens are the same or not.(with this impelementation, attacker can not read csrf token and his req is not valid in server.)
23 November 2024
20:11
Schriften
how binary search works:

function binarySearchSteps(totalItems) {
// if (totalItems <= 0) {
// return 0;
// }
// let count = 1;
// while (totalItems > 1) {
// totalItems = Math.floor(totalItems / 2);
// count++;
// }
// return count;
//or :
return Math.ceil(Math.log2(totalItems));
}
27 November 2024
00:03
Schriften
Linear and logarithmic time.

When the max numbers of each search is the same as size of the list. This is called linear time.
But if the numbers of each search is based on how many times can the list be divided to 2 , its called log time or logarithmic time.
28 November 2024
19:11
Schriften
about big 0 notaion:
it tells us how fast an algourthm is. big o is not about how much time will take that an alogorthm reaches the result, its about how many operations will take that an algorithm reaches to the result.
in simple search in a list of n items it takes O(n) operation (worst case)
in binary search in list of n items it takes O(log n) operations.
29 November 2024
03:04
Schriften
In reply to this message
factorial time O (n!)
this is a terrible and a low running alg which there is no alternative solution for it.
the travleing saleperson who wants to travel to 5 cities and wants to find the shortest route for travelling to all of them.

function salePerson(citesAmount) {
let result = citesAmount;
let remain = citesAmount - 1;
while (remain > 1) {
result _= remain;
remain--;
}
return result;
// return citesAmount <= 1
// ? 1
// : (citesAmount = citesAmount _ salePerson(citesAmount - 1));
}
21 December 2024
20:46
Schriften
about SW:
A service worker is a bit like a proxy server between the application and the browser, and it has quite a bit of power. With a service worker, we can completely take over the response from an HTTP request and alter it
3 January 2025
19:49
Schriften
regular import statement and import('/dir') :
first one load the comp in compile time and the sec one loads it on demand / on run time (layzy loading)
21:15
Schriften
About CI - CD:
continues integration: a service that make changes be tested and build automatically. It helps to speed up tests and build for safer deploy by ensuring that the new changes won’t break the codebase.
CD: continues deployment: automatically deploys your react app on production or staging env if the CI pipeline is passed.
For this service we need: version control system like gitlalb - CI-CD service like GitHub actions , circle CI , Jenkins - deployment platform: verbal - firebase or custom servers.

we need to create a workflow in the project, its a .yml file based on version control . In the file we manage what command (build , liners …) run and when they run (after push or merge some changes in demo or master
20 January 2025
20:59
Schriften
Infinity in js:
its type is number. we use it sometimes to initalize a variable with a number that is definitly bigger than any future nums that goining to be assigned to the varibale.
i.e Infinity ensures that any future re-asigining number will be shorter that our current reasigned num (which is infinity).
21 January 2025
22:45
Schriften
dijkstra alg

- make a store for distances , visited nodes , parent nodes, proccessing nodes
- initialize distances and parent: parent with null and distances with infinity
- reasigning first node distance to 0

- find the closest unvisited node
- update its neighbors distances
- find the next closest unvisited node...

- find the fastest path by backtracking through parents.

const graph = {
START: { A: 6, B: 2 },
A: { FIN: 1 },
B: { A: 3, FIN: 5 },
FIN: {},
};
function dijkstra(graph, start, end) {
const distances = {};
const visited = new Set();
const previous = {};
const nodes = new Set(Object.keys(graph));

// Initialize distances and previous
nodes.forEach((node) => {
distances[node] = Infinity;
previous[node] = null;
});
distances[start] = 0;

while (nodes.size > 0) {
// Get the closest unvisited node
let currentNode = null;
nodes.forEach((node) => {
if (
!visited.has(node) &&
(currentNode === null || distances[node] < distances[currentNode])
) {
currentNode = node;
}
});

    if (currentNode === null || distances[currentNode] === Infinity) {
      break; // No reachable nodes left
    }

    // Mark as visited
    nodes.delete(currentNode);
    visited.add(currentNode);

    // Update distances to neighbors
    const neighbors = graph[currentNode];
    for (let neighbor in neighbors) {
      const newDistance = distances[currentNode] + neighbors[neighbor];
      if (newDistance < distances[neighbor]) {
        distances[neighbor] = newDistance;
        previous[neighbor] = currentNode;
      }
    }

}

// Backtrack to find the shortest path
const path = [];
let current = end;
while (current !== null) {
path.unshift(current);
current = previous[current];
}

if (path[0] !== start) {
return { path: null, distance: Infinity }; // No path found
}

return { path, distance: distances[end] };
}

// Run the algorithm
const result = dijkstra(graph, "START", "FIN");
console.log(Shortest path: ${result.path.join(" -> ")});
console.log(Shortest distance: ${result.distance});
23 January 2025
13:06
Schriften
about useEffect hook:
According to the react documentation, the callback should either return nothing (undefined) or return a cleanup function.
14:12
Schriften
why use reqeutAnimationFrame:

this func takes a callback and call it after each frame render. so this func make updates happen based on browser refresh rate (60 fps) and sync updates with browser rendering cycle and avoid redundant updates in each frame.

import React, { useState, useEffect, useRef } from 'react';

const ScrollPosition = () => {
const [scrollY, setScrollY] = useState(0);
const ticking = useRef(false);

useEffect(() => {
const handleScroll = () => {
if (!ticking.current) {
ticking.current = true;
requestAnimationFrame(() => {
setScrollY(window.scrollY);
ticking.current = false;
});
}
};

    // Attach the scroll event listener
    window.addEventListener('scroll', handleScroll);

    // Cleanup the event listener on unmount
    return () => {
      window.removeEventListener('scroll', handleScroll);
    };

}, []);

return (

<p>Scroll Y Position: {scrollY}px</p>
);
};

export default ScrollPosition;

- the callback called before browser renders the next frame.
- it exactly call before paint process
- The requestAnimationFrame callback is scheduled after JavaScript execution but before rendering starts.
- This timing ensures:
  Any DOM or CSS updates you make in the RAF callback are applied before the next frame is painted.
  There’s no unnecessary reflows or repaints between frames, leading to optimal performance.

then the requestAnimationFrame calls before painting and get ready the update in callback and then gives the update to next render(frame)
14:32
Schriften
reqeutAnimationFrame runs after all microtasks have been processed and before the browser repaints the screen. then its MacroTask
19:15
Schriften
stopImmediatePropagation()
The event.stopPropagation() stops the event from going to the next element. All handlers associated with the current element for that particular event will still get executed. This does not happen in event.stopImmediatePropagation() where propagation stops immediately, and no event handlers execute even if they belong to the current element.
19:18
eventprogations:
when event is triggered , event passed from root down to the target element (capturing)
event reach to target and be executed (targetting)
event bubble up and all event in the way be executed (bubbling)
19:36
Schriften
about this in event listenders:
When used in event listeners, this refers to the element that triggered the event.
in general this reffers to the surrending lexical scope.

const button = document.querySelector('button');
button.addEventListener('click', function() {
console.log(this); // Refers to the button element
});
24 January 2025
02:21
Schriften
strict mode:

- gives err when create unasigned value : x = 2
- gives err when we use this.val and val is not in the lexical scope
- cant assigned prop to a non-writable obj

const obj = {};
Object.defineProperty(obj, 'x', { value: 42, writable: false });
obj.x = 10; // Throws TypeError in strict mode

it prevents silent errs like these to be ignored
it makes code more constant and predictible and hepls debugging

strict mode applies these rules in parsing. the js engine v8 or spidermonky parses codes and turns them in to AST in AST some stricter rules check the code for any dangers.
after parsing strict mode transfer these issues in runtime.
20:03
Schriften
about obj decriptors:

Object.defineProperty(obj, "key", {
// Getter for 'key' this func will run when we want access to key prop: obj.key
get: function () {
return this.\_key || "Default Value"; // Return the value of '\_key' or a default if not set
},

// Setter for 'key' this func will run when we want access to key prop: obj.key
set: function (value) {
if (typeof value === "string") {
this.\_key = value.trim(); // Validate and trim the value before setting
} else {
console.error("Invalid value. 'key' must be a string.");
}
},

enumerable: true, // Makes the property show up during enumeration (e.g., in `for...in`)
configurable: true // Allows the property to be redefined or deleted
});
25 January 2025
20:22
Schriften
react reconcilition and diffing alg:
react in every state changes creates a new v dom and compares it with old to update r dom in exact location of change. this is called reconcilation. the way react does it is diffing alg:
in diffing alg: if the root element type is changed -div => p react destory old tree and replaces with new tree. if the elment didint change react update its props.
react only compares the nodes at the same level- o(n) and not compares eveny nodes pair o(n2).
based on comparing node on the samce level react makes some assumtions if update or use old instance.
21:01
Schriften
selection sort o(n2)

function findSmallest2(arr) {
let smallest = arr[0];
let idx = 0;
for (let i = 1; i < arr.length; i++) {
if (arr[i] < smallest) {
smallest = arr[i];
idx = i;
}
}
return idx;
}
function selectionSort(arr) {
let sortedArr = [];
while (arr.length > 0) {
for (let i = 0; i < arr.length; i++) {
const smallest = findSmallest2(arr);
sortedArr.push(arr[smallest]);
arr.splice(smallest, 1);
}
}
console.log(sortedArr);
}
selectionSort(array2);

selection sort another:

function selectionSort(arr) {
for (let i = 0; i < arr.length; i++) {
let minIndex = i;
for (let j = i + 1; j < arr.length; j++) {
if (arr[j] < arr[minIndex]) minIndex = j;
}
if (minIndex !== i) [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
}

console.log(arr);
}
21:22
Schriften
quick sort

function quickSort(arr) {
if (arr.length < 2) {
return arr;
}
// choose the middleItm as pivot
let pivotIdx = Math.floor(arr.length / 2);
let pivot = arr[pivotIdx];
let left = [];
let right = [];
for (let i = 0; i < arr.length; i++) {
if (i === pivotIdx) continue;
if (arr[i] > pivot) {
right.push(arr[i]);
} else {
left.push(arr[i]);
}
}
return [...quickSort(left), pivot, ...quickSort(right)];
}
21:36
binarySearch:

function binary(arr, itm, low, high) {
// let low = 0;
// let high = arr.length - 1;
// while (low <= high) {
// let mid = Math.round(high + low / 2);
// let guess = arr[mid];
// if (itm === guess) {
// return mid;
// } else if (itm > guess) {
// low = mid + 1;
// } else {
// high = mid - 1;
// }
// }
// return "none";

// recursive way:
if (low > high) {
return "NONE";
}
let mid = Math.floor((low + high) / 2);
let guess = arr[mid];
if (itm === guess) {
return mid;
} else if (itm > guess) {
return binary(arr, itm, mid + 1, high);
} else {
return binary(arr, itm, low, mid - 1);
}
}
22:32
Schriften
a simple usage of arr.reducre 😬

const numbers = ["a", "b", "a", "b", "c", "d", "c"];
const sums = numbers.reduce((accumulator, currentValue) => {
if (accumulator[currentValue]) {
accumulator[currentValue]++;
} else {
accumulator[currentValue] = 1;
}
return accumulator;
}, {}); // initValue of the accumulator

// { a: 2, b: 2, c: 2, d: 1 }

or

const numbers = [1, 2, 3, 4, 5];
const sums = numbers.reduce((accumulator, currentValue) => {
return accumulator + currentValue;
}); // Initial value is 0
27 January 2025
23:27
Schriften

- we have 5 radio stations
- we want to start a show and we want to reach to the listeners in 10 states
- each station can cover multiple states and the states could overlap

greedy solution:

- find the station that covers states that haven't been covered
- repeat till all 10 states are covered

const statesNeeded = new Set([
"WA",
"OR",
"ID",
"NV",
"UT",
"CA",
"AZ",
"MT",
"CO",
"NM",
]);
const stations = {
station1: new Set(["ID", "NV", "UT", "CO"]),
station2: new Set(["WA", "ID", "MT"]),
station3: new Set(["OR", "NV", "CA"]),
station4: new Set(["CA", "AZ", "NM"]),
station5: new Set(["CO", "UT", "NM"]),
};
function greedySetCover(statesNeeded, stations) {
const selectedStations = new Set();

while (statesNeeded.size > 0) {
let bestStation = null;
let statesCovered = new Set();

    for (const [station, states] of Object.entries(stations)) {
      const covered = new Set(
        [...states].filter((state) => statesNeeded.has(state))
      );

      if (covered.size > statesCovered.size) {
        bestStation = station;
        statesCovered = covered;
      }
    }
    selectedStations.add(bestStation);
    statesCovered.forEach((state) => statesNeeded.delete(state));

}

return selectedStations;
}

const result = greedySetCover(statesNeeded, stations);
console.log({ result });
29 January 2025
11:11
Schriften
مصاحبه*فرانت*اند*دیوار*۱۴۰۲*تغییر*ساختار*اطلاعات.pdf
Not included, change data exporting settings to download.
420.4 KB
11:11
مصاحبه*فرانت*اند*دیوار*۱۴۰۲*جستجو*میان*اسامی.pdf
Not included, change data exporting settings to download.
255.8 KB
6 February 2025
20:45
Schriften
in programming arr or str are zero-based-indexed but in dynamic programming we're creating grids and we should consider in DP arrays are one-based inexed:
the LCS soultuion in DP:

function longestCommonSubstrDP(s1, s2) {
let m = s1.length;
let n = s2.length;

// Create a 1D array to store the previous row's results
let prev = new Array(n + 1).fill(0);

let res = 0;
for (let i = 1; i <= m; i++) {
// Create a temporary array to store the current row
let curr = new Array(n + 1).fill(0);
for (let j = 1; j <= n; j++) {
if (s1[i - 1] === s2[j - 1]) {
curr[j] = prev[j - 1] + 1;
res = Math.max(res, curr[j]);
} else {
curr[j] = 0;
}
}

    // Move the current row's data to the previous row
    prev = curr;

}

return res;
}

// Driver Code
let s1 = "";
let s2 = "ggeegeeksquizpractice";
console.log(longestCommonSubstrDP(s1, s2));
8 February 2025
21:14
Schriften
flat arr with array.reduce:

const myArr = [
[1, 2],
[3, 4],
[5, 6],
];

function makeFlat(arr) {
return arr.reduce((acc, curr) => {
if (Array.isArray(curr)) {
acc.push(...curr);
}
return acc;
}, []);
}

with while loop:

function makeFlat(arr) {
const simpleArr = [];
let i = 0;

while (i < arr.length) {
simpleArr.push(...arr[i]);
i++;
}
return simpleArr;
}
22:22
Schriften
if we difine a variable without any syntactx it becomes an implicit global varibale and we could access to it event if its difined in a functional scope. a varibale with var does not like this and if defined in fuincion scope its accecible only there:

function test() {
x = 10; // ❌ No var/let/const -> Becomes a global variable!
}
test();

console.log(x);
22:24
if a varibale difned with var in a non-functional scope it becomes a direct winow obj varibale.
22:24
about var let const 👆
22:43
Schriften
long running task like, cpu-intesive taske, fs.readfile, mirotaskst and the eventLoop it self in node env are handled(offloaded to) with Libouv:
Since there's no browser in a Node.js environment.
A C++ library that powers Node.js’s async operations.
17 February 2025
21:31
Schriften
about func.call method:
Great question! The .call() method is used in JavaScript to invoke a function with a specific value for this. Let’s break it down:

in generall when we call the someFunction without call method, the this reffers to window, but now:

function someFunction() {
console.log(this);
}

someFunction.call('kosher'); //log kosher

function createWrapper() {
return {
innerObj: {
getThis: () => this, // `this` comes from createWrapper's `this`
},
};
}

const obj1 = createWrapper();
console.log(obj1.innerObj.getThis()); // `this` depends on how createWrapper() was called

const obj2 = createWrapper.call({ custom: "I'm the wrapper this" });
console.log(obj2.innerObj.getThis()); // { custom: "I'm the wrapper this" }
26 February 2025
00:56
Schriften
About access and refresh tokens:

Access tokens are short lived (15 min) , it saved in cookies on header and sends in each req to server. When this token is expired, front send automatically the saved refresh token to the back, after its verified, back send a new access tokens. This way no logging out happens and user can be verified.

Tokens are saved in http only req and therefor JavaScript can not have access to it.
01:04
//Backend setting cookies in client browser:

res.cookie("accessToken", accessToken,
{ httpOnly: true, secure: true, sameSite: "strict" });
res.cookie("refreshToken", refreshToken, { httpOnly: true, secure: true, sameSite: "strict" });

httpOnly: true (Most Important Security Setting)
Prevents JavaScript access to the cookie.
Stops XSS attacks from stealing the token.
The cookie can only be accessed by the server (not localStorage or sessionStorage)

secure: true
The cookie is only sent over HTTPS.
Prevents attacks on unsecured (HTTP) connections.
Important in production (but must be turned off for local development if not using HTTPS).

sameSite: "strict"
Prevents CSRF (Cross-Site Request Forgery) attacks.
Ensures cookies are only sent from the same site (not from external websites).
"strict" means the cookie is never sent when navigating from another site (high security).
If "lax", it would allow cookies in safe cross-site requests (e.g., links).
01:10
const response = await axios.get("http://localhost:5000/protected", { withCredentials: true });

The { withCredentials: true } option ensures cookies are included in the request and response.
The backend validates the credentials, generates JWT tokens, and sends them as HTTP-only cookies.
The browser automatically saves the cookies for future requests.
20:36
Schriften
handling http req in react vite:
we can use axios because:

- Supports interceptors: we can set rules and handle diff situation of res or req with it. we can get token from req and presve it for future use ( if token is not in cookies and not http-only)
- we can retry req automatically when its rejected

const apiClient = axios.create({
baseURL: "https://api.example.com", // Replace with your API URL
withCredentials: true, // Sends cookies (for authentication)
headers: {
"Content-Type": "application/json",
},
});

// Request Interceptor (Adds Authorization Token)
apiClient.interceptors.request.use(
(config) => {
const token = localStorage.getItem("accessToken");
if (token) {
config.headers.Authorization = `Bearer ${token}`;
}
return config;
},
(error) => {
return Promise.reject(error);
}
);

apiClient.interceptors.response.use(
(response) => response, // Success response
async (error) => {
const originalRequest = error.config;
if (error.response?.status === 401 && !originalRequest.\_retry) {
originalRequest.\_retry = true;
try {
const { data } = await axios.post(
"https://api.example.com/auth/refresh-token",
{},
{ withCredentials: true }
);
localStorage.setItem("accessToken", data.accessToken);
apiClient.defaults.headers.Authorization = `Bearer ${data.accessToken}`;
return apiClient(originalRequest); // Retry the failed request
} catch (refreshError) {
console.error("Session expired. Please log in again.");
}
}
return Promise.reject(error);
}
);

, automatic request cancellation, and better error handling.
20:40
alse in handling http req we can use react query to cash responces. this way we dont need to req every time we back to previos page:

const fetchUser = async () => {
const { data } = await apiClient.get("/user/profile");
return data;
};

export const useUser = () => {
return useQuery({
queryKey: ["user"],
queryFn: fetchUser,
staleTime: 1000 _ 60 _ 5, // Cache for 5 minutes
});
};
20:55
we can alose use SWR instead react query but react query is more advanced and more configurable:
RQ has optimisitc updates and retry but SWR is much simpler.

with retry we can retry any req by error types or any condition. by defualt any faild req in RQ will retry 3 times:

export const useUser = () => {
return useQuery(["user"], () => apiClient.get("/user").then((res) => res.data), {
retry: (failureCount, error) => {
if (error.response?.status >= 400 && error.response?.status < 500) {
return false; // Don't retry on client errors (4xx)
}
return failureCount < 3; // Retry up to 3 times for other errors
},
});
};

with optimisic update we can update UI before any resopoce comming from server optimictically.
RQ has a mutate methot to handle that and if the req is failed we can also roll back to prev state.

import { useMutation, useQueryClient } from "@tanstack/react-query";
import apiClient from "../api/apiClient"; // Axios instance

export const useUpdatePost = () => {
const queryClient = useQueryClient();

return useMutation(
(updatedPost) => apiClient.put(`/posts/${updatedPost.id}`, updatedPost),
{
// ✅ Optimistic Update
onMutate: async (updatedPost) => {
await queryClient.cancelQueries(["post", updatedPost.id]);

        const previousPost = queryClient.getQueryData(["post", updatedPost.id]);

        // Update UI immediately
        queryClient.setQueryData(["post", updatedPost.id], (oldPost) => ({
          ...oldPost,
          title: updatedPost.title,
        }));

        return { previousPost };
      },

      // ✅ Rollback if Error Occurs
      onError: (error, updatedPost, context) => {
        queryClient.setQueryData(["post", updatedPost.id], context.previousPost);
      },

      // ✅ Refetch Data from Server After Success
      onSettled: (updatedPost) => {
        queryClient.invalidateQueries(["post", updatedPost.id]);
      },
    }

);
};
20:57
SWR does not have a built-in onMutate like React Query, but you can achieve optimistic updates manually using mutate()

export const updatePostTitle = async (postId, newTitle) => {
const updatedPost = { id: postId, title: newTitle };

// ✅ Optimistically update the cache
mutate(`/posts/${postId}`, (prevData) => ({ ...prevData, title: newTitle }), false);

try {
await apiClient.put(`/posts/${postId}`, updatedPost);
mutate(`/posts/${postId}`); // ✅ Revalidate after success
} catch (error) {
mutate(`/posts/${postId}`); // ❌ Rollback on failure
throw error;
}
};
20:59
You can customize retry behavior using errorRetryCount and errorRetryInterval in SWR
It does NOT retry POST, PUT, DELETE mutations (React Query supports this).
28 February 2025
13:06
Schriften
about import.meta.glob(dir)

react vite allows use to impotrt multiple modules from the fileSysyem:

const pages = import.meta.glob('@/pages/\*_/_.tsx', { eager: true });

// by default vite lazyload the paths if the eager true is NOT set
// remember when lazyload is on, all the module in a dir will be importer and tree shakinh is not happen.

this gives use an obj with path name as key and module as value. we can map throght this obj to get paths and modules.

It's possible to only import parts of the modules with the import options.

const modules = import.meta.glob('./dir/\*.js', { import: 'setup' })

//When combined with eager it's even possible to have tree-shaking enabled for those modules.
const modules = import.meta.glob('./dir/\*.js', {
import: 'setup',
eager: true,
})
13:18
lazyLoading and eagerLoading:
in lazy files will imported when they're needed (reducing init bundle). but in eagerLoading files are imported imidiatly in build time.
in vite when we lazyload

const pages = import.meta.glob('@/pages/\*_/_.tsx')

the value of the pages obj is a func that returns a promise and if we want to use that module we have to get it in .then ie import them manually.

setting eager to true for mediuom app is okay but as the app grows its better to lazyload to reduce the required code for initial page.
but rememer if You want instant navigation between all pages the eagerLoading might help.
3 March 2025
22:50
Schriften
about recursive or simple loop func performance:

//recursive
function sumRecursive(n) {
if (n === 0) return 0;
return n + sumRecursive(n - 1);
}

//itarative approach:

function sumIterative(n) {
let sum = 0;
for (let i = 1; i <= n; i++) {
sum += i;
}
return sum;
}

the recursive way and itarative way both have same TC - o(n) but the recursive has more SC: it is o(n) but the itarative has o(1)
so generally iterative way has better in performance due to the less space complexity and dont need any stack managemenet.
so

- itarative way uses a fixed amount of memory (usually O(1)
- recursive way can lead to stack overflow if the recursion depth is too large.
- The time complexity of recursive remains the same as the iterative version if implemented correctly, but space complexity might increase due to stack frames.
  6 March 2025
  19:10
  Schriften
  about stack and queue:

stack is first in last out and used inside functuin call stack, browser history, recursion.

function first() {
console.log("First function called");
second();
console.log("First function finished");
}

function second() {
console.log("Second function called");
third();
console.log("Second function finished");
}

function third() {
console.log("Third function called");
}

first();
// - first push to callstack, then second and then third, after execution of the third, the second func execution continues from the rest and the funcs popped off from last to start.
// First function called, sec function called, third function called, after this, js backtracks to pop off prev func from the stack and:

//sec function finishid, First function finished

queue is first in first out and used in request handling
10 March 2025
22:33
Schriften

- arr.find has o(n) tc and use simpleSeaarch
- arr.sort has o(n log n ) tc in avarage cases and worst cases and o(n) when the list is already sorted!
  arr.sort uses timeSort in modern JavaScript engines v8 (e.g., Chrome, Node.js, Edge, Firefox) and in older uses quickSort.
  Timsort is a hybrid algorithm combining Merge Sort and Insertion Sort.
  24 March 2025
  16:12
  Schriften
  document.startViewTransition simple explain:
  it takes a snapshot from the page current state and then runs dom updated (ui changes or route changes ...) and then it animate between the snapshop and the new dom update.
  we can customize the default behavior of the viewTransition animation wit setting the css related prop:

/_ Create a custom animation _/

@keyframes move-out {
from {
transform: translateY(0%);
}

to {
transform: translateY(-100%);
}
}

@keyframes move-in {
from {
transform: translateY(100%);
}

to {
transform: translateY(0%);
}
}

/_ Apply the custom animation to the old and new page states _/

::view-transition-old(root) {
animation: 0.4s ease-in both move-out;
}

::view-transition-new(root) {
animation: 0.4s ease-in both move-in;
}
16:33
Schriften
startViewTransition returns a promise with 2 methods: .ready:
this is called when the new state applies and before any animation happens.

finished resolves when the animation is completely done.
23:35
Schriften
how timeSort works:
its a combination of mergeSort and selection sort. it turns the array in to smaller chunks or subArray and sort inside these subArrays with selectionSort and then merge all these array with mergeSort. TC of this algo is:

- in worst case (already sorted arr) = o(n)
- avarage case o (n log n)
- best case o(n log n)
  28 March 2025
  18:12
  Schriften
  why using simple variables for storing data in react doesn't work:
  Because React components are just functions, normal variables won’t persist across different invocations of those functions (which React calls renders).
  3 May 2025
  12:51
  Schriften
  Docker for front end.pdf
  Not included, change data exporting settings to download.
  2.7 MB
  Docker for front end.pdf
  7 May 2025
  21:25
  Schriften
  reduce bundle size:
  code spliting:
  useing react.lazy to load compoenend when needed (on demand) and not in build time at the init js bundle. react lazy comp loaded at render time.
  lazyloading improves faster initial load => TTI use can start interacting much sooner.
  les memory usage. cause the browser doesnt need to hold all the parsed js at once.
  lazy loading pages can also be a very good idea to reduce bundle size.

tree shaking:
enure the install libs support ESM and avoid common js. cause commonJS doent tree shaked and also does not support lazyLoading.

removing dead code : with bundle analyzer we can watch moudles that are inclueded in the bundle but never have been used.
setting sideEffect: false in the lib in pacck.json: when you verified that the module hasn't anyside affects, with setting this you help module bundler to be sure it can treeshake the lib if needed.

useing lighter alternative libs: keenslider instread swiper or nanoId instead uuid.

use svg and svg optimize

ssr + partial hydration: old ssr caused issues in page transtion because the page need be fully rendered on server by navigating
but with hydration only part of the page could be ssred and the rest be fetched on the client side. ( we could use react.layzy to make thesse parts be fetched on client)
8 May 2025
14:36
Schriften
In reply to this message
react disable event pooling from 17th version. the pooling makes the handler unsutable for async tasks like async/await or setTimeout. cause the event object properties set to null and cleare after the event handler is compeleted. so now we have an synthetic event obj instance for every event we trigger. we can now have access to event properties asynchronly without needing to call event.persist()
17:39
Schriften
new Event and new CustomEvent
new Event() in browser is for creating a basic custom Event object. its very simple doesn't support payload and its for transfering simple singals.
instead the CustomEvent supports payload and more complicated structure.
we can use both of them in EventTarget.dispatchEvent.

const event = new Event("my-event");

element.dispatchEvent(event);
17:54
Schriften
Mohsen Khademhoseini 08.05.2025 17:54:08
10_Code_Challenges_to_Master_Promise_then_and_Promise_catch_by_Shuai.pdf
Not included, change data exporting settings to download.
1.6 MB
17:54
10_JavaScript_Promise_Challenges_Before_You_Start_an_Interview_by.pdf
Not included, change data exporting settings to download.
4.7 MB
23:11
Schriften
Photo
Not included, change data exporting settings to download.
1280×618, 56.8 KB
.catch in promise also returns a new promise which allows that any .then after it be executed.
23:15
Photo
Not included, change data exporting settings to download.
1280×649, 40.5 KB
in fact .then and .catch botch return a promise and tranfers the last return value to the other chained .then or .catch
23:23
const promise = new Promise((resolve, reject) => {
resolve(1);
});

promise.then(res => {
console.log('first then: ', res);
return 2;
});

promise.then(res => {
console.log('second then: ', res);
return 3;
});

promise.then(res => {
console.log('third then: ', res);
});

// log resut: 1 - 1 - 1

const promise = new Promise((resolve, reject) => {
resolve(1);
});

promise
.then(res => {
console.log('first then:', res); // res = 1
return 2;
})
.then(res => {
console.log('second then:', res); // res = 2
return 3;
})
.then(res => {
console.log('third then:', res); // res = 3
});
// log result: 1 - 2 - 3
9 May 2025
17:06
Schriften
about mono repo:
when we're using a system which handles different projects in a single repository.

- with mono repo all projects stays always sync and updated
- it makes upadate and changes faster ( all projects will changed with one commt!)
- mono repo project could access a very highly valued resources of other projects like utils and logic, basic comps, bakend api and libs.
- tools like Nx or turborepo help to manage mono repo
- in mono repo, safty is very important! staging env, code review, test-writing - storybook or...

downsides:

- lower build time, lowr CI and CD time (google built its own tool for handle build time called Bazel to deal with massive scale builds)
- tools like npm or git or webpack struggle with mono repos and companies should create custom tool or use open source tools like lerna
- harder and long onboarding for new one - so documentation is veeeery imortant
  17:36
  Schriften
  about lerna
  js/ts mono repos could use lerna. lerna is an open-source package manger with that we can link local packages acrros different prject without needing to insall them speparately. it manges also versioning
  11 May 2025
  20:35
  Schriften
  about stacking context
  its a layering system that determine how the elements should be layered related to each other.
  or:
  stacking context determins the order in which the html elements are positioned. buy default the order is:
  root element
  non positioned element
  positioned element

by default every element should obay the root stacking context (html) but when some css prop is set inside an element, a new stacking context is created by that element.
giving zIndex to an element create a new stacking context.
element that are positioned create their own stacking context, child elements insdie them onbay that statcking context but chaning z-index of that child doesn't affect the ohter element outside its parent, cause the outsiders have their own stacking context (it might be the root by default)

isolation:isolate prop
it can be used to create stacking context for an element without postioning it.
when we have an element with z-999 it might accidently apear on top of something that we dont want to, isolating it (or it parent) allows us to force that element to stay inside its stacking context

props like filter, opacity, transform, isolation can also create stacking context

https://www.geeksforgeeks.org/describe-z-index-and-how-a-stacking-context-is-formed-in-css/
12 May 2025
22:28
Schriften
in other words with z-index we can explicitly control the stacking order of html elements.

By default, a plain HTML document will have a single stacking context that encompasses all nodes. But we can create additional contexts!

An element inside one stacking context can never be compared against elements in another:
According to the rules of CSS, there is no way for us to "break free" of the stacking context. An element inside one stacking context can never be compared against elements in another.
We can still achieve the desired result, however, with a bit of out-of-the-box\* thinking.
(means we bring tooltip out of the main) we could do such thing in react bt creating portal.

When a stacking context is created, it “flattens” all of its descendants. Those children can still be rearranged internally, but we've essentially locked those children in

About isolation:
When we apply this declaration to an element, it does precisely 1 thing: it creates a new stacking context.

With so many different ways to create a stacking context, why do we need another one? Well, with every other method, stacking contexts are created implicitly, as the result of some other change. isolation creates a stacking context in the purest way possible: don't need pos zindex, filter, flex zindex and....
13 May 2025
20:17
Schriften
Diff merge and rebase
In merge the history will not be rewritten, it takes all next the steps of the main and merges with the feat branch that created from two steps before of the main and add a new commit for this.

Rebase take the whole branch and move it on top of the main branch like the whole commits belong to the main from first.
22:47
Schriften
About execution context:
The Env that js codes run and execute

Three kinds of context:
global context (window or global in node)
functional context
Eval context

It has two phases:
Creation: memory allocation and hosting happen here

Execution phase: executing codes line by line, assigning value to variables, executing funcs

Memory allocation in first phase:
Js reserve memory for variables and then assign the real value in sec phase.
18 May 2025
00:05
Schriften
about commonJs and tree shaking:
if we require and use commonJs to use a file, tree shaking will not happen. because tree shaking needs to know statically which file or data is exported (its based on static analysis ) and in commomJs the require will imports the enitre module.
00:06
also we cant dynamically import a commonJs module unless we make it as default export and its again a bad practice. but in a native ESM env we cant that at all undless we use createRequire()
00:09
How ISR Works (Simplified)
On build, Next.js statically generates pages using getStaticProps.

When a user visits a page:

If the static page exists and is fresh → it's served instantly.

If it’s stale (based on revalidate time), a background regeneration is triggered.

The updated page is saved and served for future requests.

// pages/blog/[slug].js

export async function getStaticProps(context) {
const post = await fetchPost(context.params.slug);

return {
props: { post },
revalidate: 60, // Re-generate the page **every 60 seconds**
};
}
27 May 2025
09:38
Schriften
About docker and dockerize:

Docker creates a consistent environment — it doesn’t care about the developer’s local setup.
09:40
It keeps the node version of the app stable and ensures that the app runs in a stable and safe env.
09:41
Also it is a great way for batching up the client and server side of the app and running them together locally.
For the we set image ports and image in the
docker-compose.yml file and run docker compose.
31 May 2025
20:43
Schriften
about loading css in react vite
in development:
react load all .css and module.css files in the head section inside style tags. this is render blocking but this adding gives react HMR in css codes. so react serves them as ESM and inject the style tags dynamically without bundling.

in production mode:
react vite use rollup to bundle everything even css module or tw , it minified them, cached them and store them inside a global index-hash.css file and link it inisde a link tap on top of the project with stylesheet rel.
this index-hash.css is created inside dist and it changes everytime a new style is added or changed so the ui could tell something changed and update it self.

TWIST: by default there is always one index.css in production after build but it could be more when we lazyloaded some comp.
when such comp loaded and has some styling, the style will be add in a different index-hash.css file and be linked on top.
4 June 2025
02:12
Schriften
Building.Micro-Frontendsr.pdf
Not included, change data exporting settings to download.
9.0 MB
7 June 2025
21:53
Schriften
About stack and heap:

Stack is for storing short-lived data: func calls and funcs local variable (str number)
A func be called and then popped of from stack, if too many func calls happens without popping of from stack (recursions) we face max call stack err.
This error happens after browser or node reach their call stack limit.
In chrome or node is between 10000 to 20000 call. The max is based on how much ram is in use.

Heap is for storing complex data like funcs, obj and arr or long or dynamic str. The data stored in heap will be removed by GC.
If a func has an obj and returns it and then we call func and assign it to the variable, the data will remain in heap if not, the data will be GCed.
Heap is for storing long-lived and complex data and is bigger that stack
````
