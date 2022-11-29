---
title: "WTF's Golang?"
date: 2022-13-11T16:54:03+00:00
weight: 1
aliases: ["/posts/wtfs-golang"]
tags: ["go","en","concurrency","channel","goroutine"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "/images/witch-learning.svg" # image path/url      
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: true # when using page bundles set this to true
    hidden: false # only hide on current single page
editPost:
    URL: "https://github.com/svbnbyrk/portfolio/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Go is an open source programming language that makes it easy to **build simple**, **reliable**, and **efficient** software. This is how [Golang](https://go.dev/) describes itself. 
### Language highlights :

- Started in _2007_
- Announced in _November 2009_
- Released *v1.0* in _March 2012_
- Stable release: 1.19.1 / 6 September 2022

 **Strengths**
- Memory-Managed (Garbage collector)
- Go compiles **directly** to machine code
- Fast compilation
- Concurrency
- Powerfull standart library/tool

 **Weakness**
- Function Overloading
- Inheritance
- Error Handling

You can look to [here](https://go.dev/tour/welcome/1 "A tour of GO") the **general knowledge** about Golang like syntax, usage, etc. I'd rather take a look at other great features.
### What are the best things about Golang?

- Concurrency
- Goroutines

The most exciting thing about Golang for me is the **_Concurrency_**. I want to quote from a [presentation](https://go.dev/talks/2012/concurrency.slide#5) shared by [Rob Pyke](https://twitter.com/rob_pike) in 2012. There are a few questions should I ask myself.

 **Why _Concurrency_?**

- Look around you. What do you see?

- Do you see a single-stepping world doing one thing at a time?

- Or do you see a complex world of interacting, independently behaving pieces?



That's why. Sequential processing on its own does not model the world's behavior. 

![desert](/images/desert.gif)

 **So, What's _Concurrency_?**

Concurrency is the composition of independently executing computations. Concurrency is a way to structure software, particularly as a way to write clean code that interacts well with the real world. _**It is not parallelism**_. If you have only one processor, your program can still be concurrent but it cannot be parallel.

Who saves gophers from the **difficulties(threads, semaphores, locks, etc.)** of parallelism?

### Goroutine
![goroutines](/images/goroutines.png)

You may have heard the **Goroutine** for the first time, but if you've ever print "Hello World" with Go, congratulations!. You have unwittingly used a goroutine. The `func main()` is actually the Goroutine. It wouldn't be the wrong to call it a **_lightweight thread_**. It has own stack that grows or shrinks when required (Up to 1GB on 64-bit and up to 250MB on 32-bit architectures). The minimum stack size of goroutine is just a **2MB**. As it is known, threads are controlled by **OS** but goroutine is controlled by **_own runtime_**, this makes it cheap for example it provides low cost **_context-switching_**. It's launched by a `go` statement. 

**For example:**

```
package main

import (
    "fmt"
)

func main() {
    go rohirrim("To the king!") // love this part btw.
}
```
Goroutine is an independently executing function. So how do you communicate between two Goroutines?

### Channels
**_"Do not communicate by sharing memory; instead, share memory by communicating"_**

When goroutines communicate by sharing memory, we use traditional concurrency synchronization techniques, such as mutex locks, to protect the shared memory to prevent data races. We can use channels to implement sharing memory by communicating.

![channels](/images/channels.png)

Golang provides a unique concurrency synchronization technique, **channel**. Channels make goroutines share memory by communicating. We can view a channel as an internal FIFO (first in, first out) queue within a program. Some goroutines send values to the queue (the channel) and some other goroutines receive values from the queue.



```
   // Declaring and initializing.
    var c chan int
    c = make(chan int)
    // or
    c := make(chan int)

    // Sending on a channel.
    c <- 1

    // Receiving from a channel.
    // The "arrow" indicates the direction of data flow.
    value = <-c
```
Channel can only transfer values of the element type of the channel. Channel types can be bi-directional or single-directional (T is any type)

- chan T denotes a bidirectional channel type. Compilers allow both receiving values from and sending values to bidirectional channels.
- chan<- T denotes a send-only channel type. Compilers don't allow receiving values from send-only channels.
- <-chan T denotes a receive-only channel type. Compilers don't allow sending values to receive-only channels.

Values of bidirectional channel type chan T can be implicitly converted to both type, but receive-only type and send-only type cannot be converted to each other.


We'll dive deeper in the next post. Thank you for reading. Your feedback is very important for me. 

**_To be continued..._**

#### Resources 

- https://go.dev/talks
- https://go101.org
- https://go.dev/tour