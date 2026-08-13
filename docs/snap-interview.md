##HTML questions:
- rel: preconnect in link tag: it used for external server and resources like fonts. tells the browser that we gonna use this server resourses so make a TCP connection with it => DNS lookup for finding related ip,  TCP connecttion and 3steps handshake.

- rel: prefetch and preload in link tag: when set preload, it prioritzes the resourse, browser go and download the data as soon as it sees the link. prefetch has lesser priority, we use it when we might need some thing later i'e another page. in when it used, the browser goes and fetches that link when its not busy.

- noopener-noreferrer in a and link: noopener does not allow the opened website to have access to our website with window.opener. noreferrer does not allow the opened website to know the referrer website (our site) header and name.(they can't know where the entered user came from.)

- the diff between img and picture tag. img for rendering images but picture is for reponsiveness, we can wrap our img tag with different sources of format (webp, png) or different image in mobile or desktop and let the browser decides which one to render:

```
<picture>
  <source
    media="(max-width: 768px)"
    srcSet="/hero-mobile.webp"
  />

  <Image
    src="/hero-desktop.webp"
    alt="Hero"
    width={1200}
    height={600}
  />
</picture>
```
- diff between opacity 0 and visibility hidden: opacity doent remove the element from layout but the opacity 0 can still create stacking context and is clickable and focusable. 
- about the script tag: ```<script src="/app.js"></script>``` this is the default. it can block browser from parsing html. when the browser arrives to it, stops parsing html, it downloads it, executes it and then continue to parsing. with ```defer``` browser download the script parallel with parsing but executes it after html parsing is finished.
```<script src="/analytics.js" async></script>``` this means download the script in parallel and execute it as soon as its ready. the browser only blocks parsing by executing and not the downloading process. suitable for independent script we can use this prop.(like analitics) Analytics doesn't usually need to wait for your application code.
- diff between async and defer. with async order of the script executing is not obayed but with defer, all the script will be executed in order of lines after parsing is over. 
- what is semantics: using html tags based on the content purposes. instead of using divs we use: 

```
<header>...</header>
<nav>...</nav>
<article>...</article>
<footer>...</footer>
```
## about git
- cherry-pick or ```git cherry-pick e5f1234``` when we want just a commit inside a branch to be merged with other branch we can use this command. It copies the changes from a commit and creates a new commit on your current branch
- diff between merge and rebase: rebase ruins the history with moving all the commits on top of other branch but merge respect the timing of merging branch commits with the targe branch.

## about css
- what is the diff between scaling line-height with ```line-height: 1.5 or 1.2 ... and line-height: 24px or somenumberpx?:
the first model scale line height based on font size:
```
font-size: 20px;
line-height: 1.5;

20px × 1.5 = 30px
```
but the second one is a static number

- what is display: contents: when it set on a wrapper element, it causes its children doesn't respect its layout and behave as if they're part of the parent element layout.  

```
<div class="flex">
  <div class="wrapper">
    <div>Item 1</div>
    <div>Item 2</div>
  </div>
</div>

// in this scenario if the wrapper has a display: contents classname, the items in it will be a part of flex element. this classname also inacitvate every classes like bg-color that is set to that wrapper in other word it causes the element to not have any layout anymore. we use this when we want an element to not have any layout but we want it still to have some css selector or event handler or... 
```
- the diff between rem and em: rem compute its number based html root font-size and the em compute it based on parent font-size:
```
html {
  font-size: 16px;
}

.box {
  font-size: 2rem; //32px
}
.somefucking:{
    padding: 1rem; //16px
}
```

```
.parent {
  font-size: 20px;
}

.child {
  font-size: 2em; //40px
}
```

```
.parent {
  font-size: 20px;
}

.child {
  font-size: 2em; /* 40px */
}

.grandchild {
  font-size: 2em; /* 80px */
}
```

or
```
.button {
  font-size: 16px;
  padding: 1em;
  border-radius: 0.5em;
}
```

- the diff between overflow hidden and clip: hidden cut off the element overlays out of its box but it still has its scroll container and can be scroll top or down but with clip every overlay of the box is cut off and the content cant be scrolled.

- the diff between flex-basis and width: both can be added to the flex item but when set width, it will set the size of the element horizontally but with basis we set the element horizontally if flex-row and vertically if flex-column.  but they both like each other. using flex-basis instead of width is more meaningful in flex though: 
```
.container {
  display: flex;
  width: 600px;
}

.a {
  flex-basis: 100px;
  flex-grow: 1;
}

.b {
  flex-basis: 300px;
  flex-grow: 1;
}
```
also when set both of them in the flex item, the flex wrapper consider flex basis size.
so in this case:
```
.item {
  width: 300px;
  flex-basis: 200px;
  flex-grow: 0;
  flex-shrink: 0;
}
```
the flex basis wins.

- diff between .freeze and .seal: with seal we cant add or rm props but we can modify values. with freeze we cant add/rm or modify. but both of them are shallow.
- diff between for in and for of: for of loops in the values but for in loops in index. therefor its recommended to use for in for lopping through objects (to get keys):
```
const user = {
  name: "John",
  age: 25
};

for (const key in user) {
  console.log(key);
}
```
so use for in for objs and for of for arrays.

- diff between shallow copy and deep: shallow copy, copies the obj at the first level only. and not the nested obj in there. so the copied obj at first level has a different refference from the base, but the nested obj in it has same reference with the base obj.

- how closure could cause memory leak? normally with closure we can keep the reference of a variable for using somewhere else, if for any reason we're referencing to smth that we don't need, that variable can scape garbage collection. 
```
function createHandler() {
  const hugeData = new Array(1_000_000).fill("data");

  return function () {
    console.log(hugeData.length);
  };
}

const handler = createHandler();
```
- the diff between null and undfined: generally undefined is not an assignment, its de-asigning but when using null, we're actually assigning it to a variable. a cheat in react prop: asigin a prop to null will prevent the related component to use its default value.

## About react
- what is pure component: its a component that only re-renders if its props have changed. pure components do a shallow comparison inside their props to control changes. in class component we achieved this with:
```
class User extends React.PureComponent {
  render() {
    return <div>{this.props.name}</div>;
  }
}
```
and in function comps with memo:
```
const User = React.memo(function User({ name }) {
  return <div>{name}</div>;
});
```

- the diff between babel and SWC: both are transpiler and convert JSX-TSX to js that browser understands but:
babel written in js - SWC written in rust and is much faster. SWC is newer and its plugins and ecosystem is a little smaller. SWC is used in Next by default. it supports ts like babel but doesn't type-check typscript and must do manually by tcs --noEmit. means it understand ts: when your write: ```const name: string = "John";``` it converts it to ```const name = "John";``` but it doesn't check if the types are okay.

- what is controlled and uncontrolled comps: controlled comp is when the react controls the comp but when we let dom directly controls it we have uncontrolled comp:
```
//controlled comp:

function Form(){
  function Form() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}

//uncontrolled comp:

  const inputRef = useRef<HTMLInputElement>(null);
console.log(inputref.current.value)
  return (
    <input ref={inputRef} />
  );

```
