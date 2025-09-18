# What is asyncio?

Asyncio or Asynchronous I/O is the python package to manage asynchronous programming in python. It allows concurrency(
_concurrency means allowing more than one task being handled at the same time_) in Python, which allows on one thread
each
process. So what is asynchronous programming? It means that a particular long-running task can be run in the background
separate from the main application. Instead of blocking all other application code waiting for that long-running task to
be completed, the system is free to do other work that is not dependent on that task. Then, once the long-running task
is completed, we’ll be notified that it is done so we can process the result. For example I/O operation, a RPC to an
external system. It allows the processor to cater other tasks and not wait for the pending tasks, coming back to the
original task when the same is unblocked.

In Python version 3.4, asyncio was first introduced with decorators alongside generator yield from syntax to define
coroutines. A coroutine is a method that can be paused when we have a potentially long-running task and then resumed
when that task is finished.

## Understanding Concurrency, parallelism, and multitasking

### Concurrency

When we say two tasks are happening concurrently, we mean that two tasks are happening at the same time. Take, for
instance, a baker baking two different cakes. To bake these cakes, we need to preheat our oven. Preheating can take tens
of minutes depending on the oven and the baking temperature, but we don’t need to wait for our oven to preheat before
starting other tasks, such as mixing the flour and sugar together with eggs. We can do other work until the oven beeps,
letting us know it is preheated.

We also don’t need to limit ourselves from starting work on the second cake before finishing the first. We can start one
cake batter, put it in a stand mixer, and start preparing the second batter while the first batter finishes mixing. In
this model, we’re switching between different tasks concurrently. This switching between tasks (doing something else
while the oven heats, switching between two different cakes) is concurrent behavior.

In a nutshell, in the above example it means that one person is not doing the same tasks at the same time, though both
the tasks are proceeding simultaneously. In case of computer systems this usually means that the the processor is moving
from one set of tasks( web request for example) to another while waiting for a long pending job.

### Parallelism

While concurrency implies that multiple tasks are in process simultaneously, it does not imply that they are running
together in parallel. When we say something is running in parallel, we mean not only are there two or more tasks
happening concurrently, but they are also executing at the same time. Going back to our cake baking example, imagine we
have the help of a second baker. In this scenario, we can work on the first cake while the second baker works on the
second. Two people making batter at once is parallel because we have two distinct tasks running concurrently

On the other hand parallelism, means that two workers, in the above case two bakers are doing the actual job. In case of
modern processors it would mean that multiple threads are running and utilising different cores of a processor.

#### The difference between concurrency and parallelism

> Concurrency is about multiple tasks that can happen independently from one another. We can have concurrency on a CPU
> with only one core, as the operation will employ preemptive multitasking to switch between tasks. Parallelism,
> however,
> means that we must be executing two or more tasks at the same time. On a machine with one core, this is not possible.
> To make this possible, we need a CPU with multiple cores that can run two tasks together.
> _While parallelism implies concurrency, concurrency does not always imply parallelism._

### Multitasking

Two main kinds of multitasking are discussed in this section: preemptive multitasking and cooperative multitasking.

> Preemptive Multitasking: In this model, we let the operating system decide how to switch between which work is
> currently being executed via a process called time slicing. When the operating system switches between work, we call
> it preempting.

> Cooperative multitasking: In this model, instead of relying on the operating system to decide when to switch between
> which work is currently being executed, we explicitly code points in our application where we can let other tasks run.
> The tasks in our application operate in a model where they cooperate, explicitly saying, “I’m pausing my task for a
> while; go ahead and run other tasks.”

> The benefits of cooperative multitasking
> asyncio uses cooperative multitasking to achieve concurrency. When our application reaches a point where it could wait
> a while for a result to come back, we explicitly mark this in code.

## Understanding processes, threads, multithreading, and multiprocessing

### Processes

A process is an application run that has a memory space that other applications cannot access. An example of creating a
Python process would be running a simple “hello world” application or typing python at the command line to start up the
REPL (read eval print loop).

Multiple processes can run on a single machine. If we are on a machine that has a CPU with multiple cores, we can
execute multiple processes at the same time. If we are on a CPU with only one core, we can still have multiple
applications running simultaneously, through time slicing. When an operating system uses time slicing, it will switch
between which process is running automatically after some amount of time. The algorithms that determine when this
switching occurs are different, depending on the operating system.

### Thread

Threads can be thought of as lighter-weight processes. In addition, they are the smallest construct that can be managed
by an operating system. They do not have their own memory as does a process; instead, they share the memory of the
process that created them. Threads are associated with the process that created them. A process will always have at
least one thread associated with it, usually known as the main thread. A process can also create other threads, which
are more commonly known as worker or background threads. These threads can perform other work concurrently alongside the
main thread. Threads, much like processes, can run alongside one another on a multi-core CPU, and the operating system
can also switch between them via time slicing. When we run a normal Python application, we create a process as well as a
main thread that will be responsible for running our Python application.


 

