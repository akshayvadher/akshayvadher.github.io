---
title: "Why Go"
date: 2022-04-29T17:34:52+05:30
draft: false
tags: ["tech", "go"]
categories: ["tech"]
author: ["Akshay Vadher"]
summary: Why Go lang. What are the feature I like the most.
cover:
    image: "logos.jpg"
    alt: "Go Logo"
    caption: Go Logo"
    relative: true # To use relative path for cover image, used in hugo Page-bundles
---

In another [post](/posts/the-programming-language-i-am-excited-to-use/), I described what are the criteria I would use to use to select a programming language. I chose `Go` as the primary one. 

However, after using it, those are not the only thing I like about Go. Here is the list of things I like about Go that stand out. 


## Go Routines
**This is the biggest thing**
`Java` code is synchronous, if we want to have async processing then we have to use Reactive Programming (which is the hardest paradigm I have learnt). Every new request in java creates a new OS thread - which takes up too many resources.

`JavaScript` uses `async` and `await` to accomplish this. Same for `c#` and `rust`. 

`Go` does async IO operation by default, you don't need to explicitly write anything to achieve async. 

Go Routines are awesome. It creates lightweight threads (which are not related to OS threads) hence we can create thousands of them without worrying about resources. 

[Case study]
I wanted to do performance testing. I started using [JMeter](https://jmeter.apache.org/) but soon I had to have multiple instances running just to do performance testing. Then I chose [Gatling](https://gatling.io/) because of its async actor model; it was nice but the setup process was a bit tedious. Then I came across [k6](https://k6.io/), it makes use of go routines the best way, now I could generate the same amount of traffic from my local machine. 

[Case study]
We made a mistake in our Java code. There was async operation that had to be started after 2 seconds. So we added `Thread.sleep(2)`. Even though it was async, it created threads and (Little did we know) there were apparently thousands of such requests, hence our "async" operation crashed the whole server. That can never happen in Go. 

## Best of everything
For **readability** use **python**

For **performance** use **rust**

For **everything** use **java**

For **fast delivery** use **python, javascript**

Notice how Go is not there in any of choice? It is because Go is #2 in everything.

If you use Python then you compromise performance, if you use C then you compromise readability. But if you chose Go, then you get the best of everything.

*It is easiest to write clean and performant code with GO (and fewer ways to go wrong)*

## Minimal keywords
Go doesn't have a rich set of keywords. 

For example, other programming language has `while`, `for`, and `do while` for loops; `Go` has only `for`. 

Go doesn't have ternary operator, because it has `if`. 

## Formatting
I personally have some issues with Go formatter. However, *I love the fact that go has formatter*.

The formatter is built inside Go lang. So every code in Go across geography and projects is formatted equally.

_+clean coding_

## Easy learning curve
Based on the above two points, since it has minimal keywords hence there are minimal ways something can be achieved and the code is formatted the same way, it is easy to learn Go. 

## Compiler
If a variable is not used but declared or the import is not used but declared then it does not allow to compile. 

Along with that, the compiler is one of the *fastest*. (as compared to other languages where we need to integrate sonar to get formatting or unused variable issues. These things take time, while Go compiler does all those things blazingly fast)

_+clean coding_

## Testing
Go has testing, coverage, and benchmarking in built.

## Statically typed
So you don't get surprises in PROD

## Smaller binary
Since it compiles to assembly directly, it is only one library and we don't need any dependency or need to install any software (I am talking to you JDK, Python, and NodeJs) to run the Go binary. 

In fact, I've seen that binary running inside `scratch` container. That means that it does not even require proper OS (almost).

My Java Spring project was 50 MiB jar file (plug OS plus JDK) but the same Go program was having 15 MiB 

## Faster startup
I have seen Go projects starting as fast as python or nodejs.

My Java Spring project took 30 seconds to start but the same Go program took 5 seconds.

## Smaller resource footprint
Because of the above reasons, it requires minimal resources to run

My Java Spring project took 50+ MiB of RAM after start but the same Go program consumed 5 MiB.

## Cloud Ready
Because of the above reasons, it is best suited for cloud deployment

Many (if not most) cloud tools are created in Go. Examples, Kubernetes, Docker, OpenTelemetry, Sops, CockroachDB, Consul, Hugo, Terraform, etc.

## Dependency
You don't have to import any binary to the project, Everything is source code. You just provide github link and go will fetch sourcecode and make the dependency available.

Since, everything is source code (and no class), the final binary will have only code available that are used. (Compare this with java, where even if you use only one method of a utility library, but if the jar file is available in dependency then it will include in final binary and the every class from that utility potentially can be loaded in JVM)

## Immutability
What do you think output of the following code?
```go

account := Account{InitialBalance: 50.0}
account.Add(50.0)

fmt.PrintF(account.Balance())

```

Do you think output will be `100.0`? Then, you are wrong. Go code is immutable by default, you either have to assign it to a new variable or pass as a pointer

## Better pointer
Sometimes it is better to have pointers for performance reasons. 

Even in that case, it does not allow us to do pointer arithmetics. 

## IDE
VS Code has plugins that work like charm. IntelliJ GoLand is (paid) awesome tool. 