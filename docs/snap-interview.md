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