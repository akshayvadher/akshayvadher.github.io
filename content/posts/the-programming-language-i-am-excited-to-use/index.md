---
title: "The Programming Language I Am Excited to Use"
date: 2021-06-12T01:14:23+05:30
draft: false
tags: ["programming", "language", "tech"]
author: ["Akshay Vadher"]
categories: ["tech"]
weight: 1
Summary: "When you starting a new project, choosing a programming language is a hard choice. Here is Here is my take."
cover:
    image: "markus-spiske-gcgves5H_Ac-unsplash.jpg"
    alt: "programming lauguage image"
    caption: programming lauguage image"
    relative: true # To use relative path for cover image, used in hugo Page-bundles
---

![programming lauguage image](markus-spiske-gcgves5H_Ac-unsplash.jpg)

When you are starting a new project, choosing a programming language is a hard choice. Here is my take.

On one hand, you might want to choose a _cool_ language but on another hand, you might want to choose a _stable_ language. 
## For 
Web servers or any _general-purpose production_ system

_Disclaimer_

_Before you read further, I want to clarify that languages and frameworks are just tools, they don't guarantee success, the way you design and code your system makes all the difference, tools will just help you ease the process if used correctly._

---
## My criteria
* Static typing 
* Compiled 
* Good community support 
* Good libraries 
* Good frameworks 
* Functional 
* Memory management 
* Easy (relatively not steep learning curve) 
---
## My criteria - language choice
**Static typing** (Because error-proof, Performance optimization)

Java, C, Rust, Go (sorry python and javascript)

**Compiled** (Performance, Memory)

Java, C, Rust, Go

**Good community support** (Don't want to be alone using the best programming language)

Java, C, Rust, Go, Python, Javascript

**Good libraries** (Don't want to reinvent the world)

Java, Javascript, Python, Go

**Good frameworks** (Library is okay but full fledge framework is required!)

Java, Javascript, Python, Go(Still evolving)

**Functional** (I am not a rigid OOP guy)

Javascript, Go

**Memory management** (As they say, if you want to make a pie from scratch, you must first create the universe. C is good but Assembly is best. I need productivity.)

Java (Nearly there), Javascript (lousy), Rust (Awesome), Go

**Easy** (relatively not steep learning curve) (Need talent already knowing lang or can be learned easily)

Python, Javascript, Go

## My choice
_**`Go`**_ (easy, good syntax, static typing and compiles fast, many libraries, menial resource consumption)

Other reasons apart from mentioned above
* **No magic code** (If you add `@Transactional` in spring, it takes care of starting, ending, and committing your transactions. It is magic. But it is double edged sword. It can do harm if not coded properly. Go is IdiotProof) (Also it is hard to master the _magic_ code. It would take weeks or months for anyone to learn Spring annotations or Ruby coding styles.)
* Minimal resource consumption (CPU, memory - spring takes 100+ MiB to start)
* Opinionated code (There are only minimal ways you can code something - makes it easy to manage a large team and codebase)
* Great threading (If you spin off 1000 threads in java with `Thread.sleep(10 * 1000)` then your app will become unresponsive. That doesn't happen with goroutines. At least it is not as bad as java)
* Many cloud native and open source tools are written in go. [kubernetes](https://kubernetes.io/), [docker](https://www.docker.com/), and [sops](https://github.com/mozilla/sops) are some examples
* More comprehensive list about other features of Go is listed in [other post](/posts/why-go)


What I don't like about Go?
* A solid framework like spring ([gin](https://github.com/gin-gonic/gin) is available though! Not sure how good is that). 
* Module management (Now they have!) 
* No generics (Maybe that is for good!) (update, now they are adding that too) 
* Extra things like liquibase integration (There are ways, but no out of box ways)

_Edit 1_

_**`Kotlin, spring-native/micronaut, and GraalVM`**_ (Maybe)
> The day `go` will have all features as java, java will be as fast as go 
>
> \- _Graeme Rocher_ (creator of Groovy, Grails, Micronaut)

With GraalVM & spring-native or micronaut, we get compiled code

With Kotlin, we get awesome syntax, functional support within Java ecosystem. 
Also, with reactive java, we can solve threading issues. Reactive itself is hard though. 

So maybe **_Kotlin, spring-native/micronaut, and GraalVM_**. Depends on the preference of other stakeholders, existing knowledge, etc. 
	
---
## Honorary mentions

**Python**: Easy  

However, I think pandas, numpy, jupyter notebook, and usage from non-coding background users are the reasons for python's popularity

Good to start but not good performance/memory wise in production

Contrary to popular belief _I don't like python_. Because you need javascript in frontend for sure, some compiled lang in backend for sure then why learn a new language, use either of them - use max two!

Huge respect though. Easiest to get started with. Not chosen because I am searching for prod server language.

**Java**: Almost chose.

You go anywhere, you find java. You need to do anything, you can do it in java. The best thing, you don't need to depend on any other languages like python/javascript which are just a wrapper of C code

Not compiled. Still needs relatively higher memory - this is the reason I didn't choose it, bit slower than compiled - at least I have been told so

**C**: Best. But when I need a needle I won't use a sword.

**C++**: Controversial. Linus doesn't like it. Anyways almost like C.

**Rust**: Awesome memory management.

Doesn't shine when need things faster - from my 30k feet view (correct me if I am wrong).

Also not good at frameworks.

**Javascript**: Never thought it would become so popular.

Easy.

You can do almost anything. Hugely error prone, lousy memory management

However, bootstrapping doesn't require too much memory (It sounds crazy given the fact that it has to call C APIs at runtime!). For simple programs, it takes less than 100MBs as compared to java which requires 500MBs. Even if javascript requires chrome engine to work. I have chosen this for simple rest APIs or simple kafka consumers because of best time to market.

Not to forget almost the _best event based paradigm_. Love it for IO.  

**Typescript**: Huge fan.

Don't like it because it still compiles to javascript. Otherwise easy, great tooling, great community support. Great overall.

_The day typescript will have its own compiler, I will use this._

**Kotline, Scala, Groovy**: What typescript is for javascript, these languages are for java

**Clojure**: Because of Lisp. However not sure much. Still compiles to java!

**C#**: Java's brother (or Sister!). I am anyways an opensource guy.

**PHP**: Are they still using it! Wordpress. If you remove wordpress never seen PHP anywhere. I don't think facebook still uses it.


##### Credit
Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
  