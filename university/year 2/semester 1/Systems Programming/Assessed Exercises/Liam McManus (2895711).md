#sp

***Just a heads up before you read any further, my Obsidian notes are set to American spelling, and I can't figure out how to change it. As you can probably tell already most words in this document follow American spelling. Let's just go with it and assume SpaceY is an American company***

---
# 1. Intro
For this new project, it's worth taking some time before we get started to think about the best tools for the job. In my opinion, the top three contenders are **Rust**, **C**, and **Go**, each offering their own advantages. **C** for its unmatched performance and the team's prior expertise, **Go** for the team's familiarity with it and it's simplicity. While our team has significant experience in **C** and **Go**, I also propose we consider **Rust** for its memory safety and concurrency model. I'll try my best to thoroughly compare them to figure out the most suitable option for moving forward.
# 2. Language Analysis

## 2.1 Concurrency and Synchronization
In chatting with the hardware team they explained the satellite has 1,326 sensors, each requiring its own processes to run concurrently in near real-time. This means the programming language we choose must support efficient, sustainable concurrency and synchronization.
### 2.1.1 Rust
**Rust** provides a robust set of tools for managing threads through its **Standard Library** in the `std::thread`. Creating threads is as simple as just calling `thread::spawn` and due to Rust's **[Ownership Model](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)**, which enforces harsh rules on variable access and memory management during compile time, mutable data cannot be shared across multiple threads without proper handling (I'll go over this a bit more in-depth later, [[#2.2.1 Rust]]). This prevents almost all race conditions all during compile time.

For thread-to-thread communication, **Rust** has support for `channels` through `std::sync::mpsc` ([Multiple Producer, Single Consumer](https://doc.rust-lang.org/std/sync/mpsc/)), `channels` in **Rust** are used to transfer data between threads safely and efficiently, these consists of a **sender** and a **receiver**, where data can be sent through the channel and when received it will transfers ownership.

Shared data can also be managed with functions like `Mutex` for locking and `Arc` for shared ownership of mutable data. Also a good thing to add, **Rust** is great at handling async code with `async` and `await`, making it easy to handle smaller lightweight tasks.

**Rust** docs are incredibly detailed and very in-depth, if you are more curious on how this works the section on Fearless Concurrency is a great read ([The Rust Programming Language, Fearless Concurrency](https://doc.rust-lang.org/book/ch16-00-concurrency.html))
### 2.1.2 GO
**Go** has built-in support for concurrency using `goroutines`, These are lightweight and simplified implementations of threads, `goroutines` make it incredibly easy to execute multiple tasks concurrently by simply calling `go func()` ([GO.dev, Concurrency](https://go.dev/tour/concurrency/1)). 

However the simplicity does introduce a few challenges, especially when it comes to managing threads, due to it not having a direct `join()` function like threads in other languages. Instead, you'll have to use a `sync.WaitGroup` to keep track of the number of running `goroutines` and then wait for them to complete one by one. 

```go
var wg sync.WaitGroup
wg.Add(1)
go func() {
    defer wg.Done()
}()
wg.Wait()
```

The lack of this returning and joining functionality means the only way to handle data in threads is through message passing - this is once again handled through `channels`, similar to [[#2.1.1 Rust]]'s implementation but once again heavily simplified this is essentially a variable you can pass into a thread that enables sending and receiving of values between threads.

```go
a <- b // Send variable b to channel a.
c := <- a // Receive from channel a and assign value to variable c.
```

This is more of a design choice that **GO** sticks by: "Do not communicate by sharing memory; instead, share memory by communicating" ([The GO Blog, Share Memory By Communicating](https://go.dev/blog/codelab-share)), this is seen as a more elegant way of handling data, avoiding the pain of locking variables and race conditions.
### 2.1.3 C
**C** allows for concurrency through **`POSIX Threads`** (`pthreads`), which are highly efficient and give a ton of control to developers. However, this comes at the cost of being incredibly error-prone due to the freedom and responsibility the language places on developers.

Developers must manually manage thread creation, synchronization, and termination. This level of control allows fine-grained management of resources and optimization. However, the complexity of safely implementing threading and avoiding the classic faults like deadlocks and race conditions makes it a double-edged sword.

"With great power comes great responsibility." (Benjamin "Ben" Parker)
### 2.1.4 Comparison

- **Rust**: Efficient threads with definite safety during compiling but will have a steeper learning curve due to these harsher rules.

- **Go**: Simple, Agile and Easy-to-use threading although less control and some code gymnastics to do trivial threading functions in other languages.

- **C**: High performance but incredibly prone to human error and requires tons of manual management of threads and shared resources.
## 2.2 Memory Management
Efficient memory management will be massively vital to the satellite, due to the importance of efficiency and the reliability needed for data coming from sensors. The programming language must have robust and efficient memory handling, minimizing risks like leaks or undefined behavior.
### 2.2.1 Rust
I mentioned it previously **Rust** enforces memory safety during compiling through the its **[Ownership Model](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)**, this almost completely removes the risk from Memory Leaks and Null Pointers without relying on the less efficient garbage collection as seen in most languages such as **Python**, **Java** and **Go**. 

Using this developers will have to define ownership over a variable and move ownership when needed, this ensures that at any given time, there is a single clear owner for a variable preventing any unsafe memory access. Also, **Rust** has very strict rules for borrowing references (`&T` for immutable and `&mut T` for mutable) which makes sure that mutable references cannot be referenced and shared simultaneously.
### 2.2.2 GO
**Go** uses the **[Go Garbage Collection](https://tip.golang.org/doc/gc-guide)** to automatically manage memory, this means as a developer you don't' need to manually allocate or free any memory, this makes development a lot faster and helps avoid certain issues like memory leaks or accessing protected memory, which are both very common errors in **C**. Although **Go's Garbage Collection** isn't all good, it can still have quite a severe hit on performance in applications that need very fast or real-time processing, while this makes the language a lot faster to develop in it may be a deal breaker for this project.
### 2.2.3 C
**C** gives full control to the developer for **Memory Management** through functions like `malloc` and `free` although like before this requires a lot of attention to get right, if managed correctly, **C** can offer incredibly high performance, but any errors in memory management could be critical, especially in a high-stakes environment like our satellite system.
### 2.2.4 Comparison

- **Rust**: Ensures memory safety at compile-time without anything extra happening at runtime, making it both safe and efficient.

- **Go**: Simplifies memory management through garbage collection, making development easier but sacrificing some performance.

- **C**: Offers complete control and maximum efficiency, but requires careful attention to avoid errors, increasing the risk of human error.

# 3. Comparisons

## 3.3 Current Capabilities and Learning Curve
**Rust** offers exceptional safety guarantees and performance, but its learning curve is steep (very steep), specifically for developers used to languages like **C** or **Go**. Getting used to **Rust's ownership and borrowing model** takes time and effort, which will slow development in the short term. On the other side, **Go** has a more intuitive syntax and given our experience means we can develop much quicker but obviously with a hit in the long to control and efficiency. **C**, while giving us unmatched control and best in class efficiency, places a heavy burden on developers to avoid critical errors, making it a less appealing choice for a high-risk project where reliability is must.
## 3.4 Project Requirements
The satellite project's needs real-time, low-latency processing of data from 1,326 sensors that each require precise memory and resource allocation. **Go**, with its garbage collector, simplifies development but may struggle to meet efficiency requirements. **Rust**, on the other hand, provides the low-level control necessary to manage memory and performance effectively, making it uniquely suited to this environment. **C** could meet these technical requirements but introduces higher risks due to its lack of built-in safety features.
# 4. Recommendation
After a careful evaluation, I recommend **Go** for its ease of use, fast development, and the team's existing skill in using it. Its lightweight concurrency model and simplicity will mean the team can focus on the higher level logic rather than the intricacies of thread safety or memory management.

That being said I'm still up for discussion **Rust** is a very compelling alternative, especially if performance, safety, and long-term maintainability are prioritized and we are willing to invest time in overcoming its learning curve, **Rust** could provide unmatched reliability and efficiency for this project.
