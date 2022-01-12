## What is concurrency?

Concurrency is performing multiple tasks at the same time. The number of tasks being performed at the same time is dependent on the number of cores a processor has. Mores cores = more tasks that can be performed.

## What are threads?

Tasks on a processor are executed on threads. Each thread has a number of tasks in line for it to perform. 


You can think of cores being a highyway with threads being each individual lane on said highway, and each vehicle being a task needing to be performed.

## Main and background threads

The main thread in iOS is a fast thread that handles things such as UI operations. The background threads perform time-heavy tasks such as network requests. We want to keep the main thread clear of time-heavy tasks so that the UI in your application is fast and responsive. 

You can think of the main thread as being the express lane on a highway, and the other congested lanes as background threads with many more tasks being performed.

## Grand Central Dispatch & NSOperation Queues


## Serial & Concurrent Queues

The serial queue operates as a first-in-first-out queue. Each task is executed one at a time, in order. 
The concurrent queue still operates tasks in order, but tasks do not have to wait for the for the first operation to get executed.
For example: 
```swift
//Serieal Queue
//   --4--3--2--1-->


//Concurrent Queue
--1-->
--2-->
--3-->
--4-->
```
In the serial queue, 1 has to execute and finish before 2, and 2 before 3, etc.  
In the concurrent queue, the tasks still execute in order, so 1, then 2, then 3, then 4. But each operation may finish in a different order. If 1 has a time-heavy task, such as a network call downloading images, and 4 is just downloading text, then 4 will finish before 1.

## When to use a serial queue vs a concurrent queue?

Serial queue operates in a predictable execution order. You can prevent race conditions.  
Concurrent queues operate faster, but are unpredictable. May cause race conditions.

## What are race conditions?

A race condition occurs when two or more threads have access to shared data, and try to make changes to that data at the same time. Due to the way concurrenct queues work, you won't know when a thread will be finished with the data. The threads are 'racing' to use the shared data. In order to prevent race conditions, you can implement locks and semaphores.
