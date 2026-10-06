## what is module federation
- its a concept highly related to micro frontend
- we have two types of app: remote app where the packs, deps or components are and a host app, where we wanna use these things
- module federation allows us to use these things at run time with making a req to the remote app and get them
- the huge diff between this and make the modules an npm pack is: with npm pack we need to install pack and rebuild when ever a module is updated
- in module federation we just get module at run time.
- then in npm package we need re-install - rebuild and redeploy 
## SOLID principles
- single responsibility: separating logic, tranforming data, fetching data, ui from each other. a ProfileUser comp shouldn't do all these it self
- comp must be opened for extension and closed for modification: it means we better better handle conditions and staus of a btn comp inside it and not doing like this
```
if (type === 'primary') {
   // ...
}

if (type === 'danger') {
   // ...
}

if (type === 'success') {
   // ...
}
```
instead we do:
```
<Button variant="primary" />
<Button variant="danger" />
<Button variant="success" />
```
we can explain it like the OOP programming. classes consist of different method based on the nature of what they describe.
- don't pass comps what they don't need: passing the whole user data to a comp that only displays name.
- don't bring low level (based logic or ui) in a high level code. don't use axios inside the comp. don't use core btn inside the page comp.
- use server in next lets us to call func, logic, comp directly on server without exposing them to client

## about react fiber
- before the rendering proceess of react was unstopable. but react introduced fiber. each react element has its own fiber which contains information about when to render and when to reconcie. so with this change, rendering became interrupt and react can Prioritizing updates. concurrent rendering is the other thing thad made with fiber.