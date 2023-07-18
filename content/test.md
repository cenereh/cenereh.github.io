+++
title = "Understanding Thread Scheduling in the Windows Kernel"
date = 2023-07-17
draft = true
[taxonomies] 
tags = ["Windows", "Kernel", "Threads", "Scheduling"]
+++

The Windows operating system is a complex system with various components, and one of its critical aspects is the scheduling of threads in its kernel. Thread scheduling is a fundamental process that allows the Windows operating system to multitask, running numerous applications and processes concurrently. In this blog post, we'll dive into the basics of how Windows handles this scheduling.

<!-- more -->

## What are Threads?

Before we get into scheduling, let's quickly define what a thread is. In computing, a thread is the smallest unit of execution within a process. A single process can have multiple threads, all executing instructions concurrently.

![Thread illustration](/images/thread-illustration.png)

## How Does Windows Schedule Threads?

The Windows operating system uses a priority-driven, preemptive scheduling system. Here's what that means:

### Priority-Driven

Each thread is assigned a priority level, ranging from 0 to 31, with 31 being the highest. The priority level determines the order in which threads are scheduled. Higher-priority threads are given preference over lower-priority ones.

### Preemptive Scheduling

Windows can interrupt or preempt a currently executing thread to give CPU time to a higher priority thread. This ability is crucial in ensuring that high-priority tasks (like system processes) can run without being hindered by lower-priority tasks.

## Thread Priorities and Levels

Windows divides the thread priority levels into six classes:

- Zero: This is the lowest priority level and is used for specific system threads.
- Idle: These threads run only when the system has no other threads to run.
- Normal: This is the default level for most threads and ranges from levels 1 to 15.
- High: These are used for threads that must respond to time-critical events.
- Real-time: This is the highest priority class and ranges from levels 16 to 31. These are reserved for threads that manage the most time-critical tasks.
- Variable: Priorities 1 through 7 are dynamic and can be adjusted by the kernel to favor background tasks.

Remember, it's not recommended to manually change a thread's priority unless necessary, as it can lead to issues like priority inversion or starvation.

## Thread Quantum

A thread quantum, also known as a time slice, is the amount of uninterrupted time a thread gets to execute on the CPU. The length of the quantum varies depending on the version of Windows and the nature of the system (workstation or server).

## Conclusion

Understanding how the Windows kernel schedules threads is crucial in grasping how the operating system manages resources. While this post only scratches the surface, it's a starting point in understanding this complex but vital aspect of the Windows operating system.

Stay tuned for more posts on Windows internals, and feel free to ask any questions in the comments below!

## Random code test
```c++
int a = 0
int b = 1
```

## Testing blockquotes
> ⚠️ smoking nic and sucking dick baby

## Testing tables
| colonna 1 | colonna 2 | a   | s   | dd  |
|-----------|-----------|-----|-----|-----|
| sadas     | d         | sad | asd | asd |
| e         | e         |     |     |     |
|           |           |     | x   |     |

## ferrari albania
![qifsha ropt](/images/test.jpg "qifsha tirana qifsha milano")

---

References:

[Windows Internals, Part 1: System architecture, processes, threads, memory management, and more (7th Edition) - Pavel Yosifovich, David A. Solomon, Alex Ionescu](https://www.amazon.com/Windows-Internals-Part-architecture-management/dp/0135159941)
