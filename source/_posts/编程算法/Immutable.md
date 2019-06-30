---
title: immutable data
date: 2019-06-23 08:03:00
tags: [Immutable, immer]
---



Immutable data

> Once we've created it and it never changes

# why

but why we need immutable data？

Functional programming （FP）

- rejecting side-effects
- mutability - in-place changes to data - helps avoid a lot of headaches

but when you refuse to mutate objects, you have to create **a whole new object** each time something changes, which can slow things down and eat up memory, making functional programming seem inefficient



"immutable data structures" === "persistent data structures"



# how

use `const` ?

like `const a = '123'`

Yes ,that is immutable data

but , how about `const obj = { a: 1 }`

You can change `obj.a` like `obj.a = 2`



In javaScript, there are some really great libraries out there to help you

- Mori.js
- Immutable.js
- Immer.js



# immer

![immer logo](https://github.com/immerjs/immer/raw/master/images/immer-logo.png)

Immer (German for: always)

> Immer is a tiny library that makes it possible to work with immutable data in JavaScript in a much more straight-forward way by operating on a temporarily draft state and using all the normal JavaScript API's and data structures.

Immer has a few unique features:

- Supports arbitrary, deep modifications in immutable data trees
- Strongly typed
- Uses JavaScript native data structures, no new API to learn
- Automatically freezes any data that is produced

![immer](https://github.com/immerjs/immer/raw/master/images/hd/immer.png)

## API

The Immer package exposes a default function that does all the work.

```
produce(currentState, producer: (draftState) => void): nextState
```



## Example



```javascript
import produce from "immer"

const baseState = [
    {
        todo: "Learn typescript",
        done: true
    },
    {
        todo: "Try immer",
        done: false
    }
]

const nextState = produce(baseState, draftState => {
    draftState.push({ todo: "Tweet about it" })
    draftState[1].done = true
})

console.log(nextState.length, baseState.length) // 3 2

console.log(baseState === nextState)  // false


console.log(baseState[0] === nextState[0]) // true , because not change
console.log(baseState[1] === nextState[1]) // false , because change 


```

Note that the producer function doesn’t return anything, the only thing that matters are the changes we make.



## Immer or ImmutableJS





## Currying

Ok. One last feature: So far we have always called `produce` with two arguments, the `baseState` and a `producer` function.

 However, in some cases, it can be convenient to use partial application. It is possible to call `produce`with just the producer function. 

This will create a new function that will execute the producer when it’s passed in a state. This new function also accepts an arbitrary amount of additional arguments and passes them on to the producer.

```javascript
// mapper will be of signature (state, index) => state
const mapper = produce((draft, index) => {
    draft.index = index
})

// example usage
console.dir([{}, {}, {}].map(mapper))
//[{index: 0}, {index: 1}, {index: 2}])
```

[React](https://reactjs.org/docs/react-component.html#setstate) `setState` can accept function

```javascript
/**
 * Classic React.setState with a deep merge
 */
onBirthDayClick1 = () => {
    this.setState(prevState => ({
        user: {
            ...prevState.user,
            age: prevState.user.age + 1
        }
    }))
}

/**
 * ...But, since setState accepts functions,
 * we can just create a curried producer and further simplify!
 */
onBirthDayClick2 = () => {
    this.setState(
        produce(draft => {
            draft.user.age += 1
        })
    )
}
```

## patches



## How does Immer work?

1) [Copy-on-write](https://en.wikipedia.org/wiki/Copy-on-write). 

2). [Proxies](https://developer.mozilla.org/nl/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

![](https://cdn-images-1.medium.com/max/1600/1*bZ2J4iIpsm2lMG4ZoXcj3A.png)

![](https://cdn-images-1.medium.com/max/1600/1*Lyw8BfTTS3AbdLEDtvJvnA.png)

as soon as you try to change something on a proxy (directly or through any API), it will immediately create a shallow copy of the node in the source tree it is related to, and sets a flag “modified”. From now on, any future read and write to that proxy will not end up in the source tree, but in the copy. Also, any parent that was unmodified so far will be marked “modified”.

When the producer finally ends, it will just walk through the proxy tree, and, if a proxy is modified, take the copy; or, if not modified, simply return the original node. This process results in a tree that is structurally shared with the previous state. And that is basically all there is to it.



### No proxies?

Proxies are available in all recent browsers. But still not everywhere. The most notable exceptions are Microsoft Internet Explorer and [React](https://hackernoon.com/tagged/react) Native (< v0.59) on Android for Android.  In such cases, Immer will fallback to an ES5 compatible implementation which works identical, but is a bit slower.

```javascript
Object.defineProperty()
```

Inspire from Vue