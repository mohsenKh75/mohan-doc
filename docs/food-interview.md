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

- BBF: imagine frontend needs some data from user - basket - orders and ... . instead of requesting multiple services from backend to get these data, backend can implement a layer and via an api get me what i need.

- percentile in sentry: what is smth like P40 = 500ms => means 40% users for example get the loaded page in 500ms and other get it in more that 500ms
- useSyncExternalStore: we use this in those cases that the source of data is outside of react: for example when we want to use some window obj props like navigator or locastorage. when we want to create a publish subscribe method for connecting data to framework different parts. it lets us to subscribe the data outside of react:
```
let count = 0
const listeners = new Set<() => void>()

const store = {
  getSnapshot: () => count,

  subscribe: (listener: () => void) => {
    listeners.add(listener)

    return () => {
      listeners.delete(listener)
    }
  },

  increment: () => {
    count++
    listeners.forEach((listener) => listener())
  },
}
```
then: 
```
import { useSyncExternalStore } from 'react'

function Counter() {
  const count = useSyncExternalStore(
    store.subscribe,
    store.getSnapshot
  )

  return (
    <div>
      <p>{count}</p>
      <button onClick={store.increment}>
        +
      </button>
    </div>
  )
}
```
it makes it easier to work outside of react for example we don't need to handle unsubscribe manually, react does that for us.

- Docker: what is docker image: when we build the project with docker the image will be exposed. image contains the info related to how to run the app: node v, app dir , copy .. , run with pnpm or... .  ```docker build -t my-next-app .``` => image

- docker container => when we run the image, an instance will be created from it that called container. ```docker run my-app``` 
- docker compose => each app could have multiple container for its different services (front back sql). we can run each of these separately and create containers manually. also we can have a docker compose.yml file which we define those config there and let docker run the containers for us. ```docker compose -up``` 
- when writing dockerfile, its better to first add the pack.json and npm install first and then copy the app:
the do: docker process the Dockerfile from top to btm and creates a layer for each part: .lock.json, pack.json and app and also cache what it processed. 
so its better to first copy lock.json, deps and command to install and then copieng the app. 
smth like this is not good practice:
```
COPY . .

COPY package.json package-lock.json ./
RUN npm install
```
in this case when the change is only related to a Button, docker copy the project again but also run the npm install, while it could be better if first handle the pack and lock and npm install and let docker re-use the cached data of them.

- diff between any and unknown: any means we don't know the type and we say ts that don't complain when we want to access the variable:
```
const x: any = "hello"
x.p //ts doesn't cmplain
//x could be anything even when we assign it to smth
``` 
but unknown is safer. we can't assign its variable to a value, without narrowing its type:
```
let value: unknown = "hello"

value.foo() // ❌ Error
value.bar() // ❌ Error

//correct with narrowing:
if (typeof value === "string") {
  console.log(value.toUpperCase()) // ✅
}
```
- dep inversion: a principle of SOLID: high level code/modules shouldn't depend directly on low-level code. 
- what is peer dep: when the installing pack expect that the host app it self provides a specific pack, it defines that pack as peer dep. for example MUI has the react as its peer dep. so the react will not be installed again just for that lib. 