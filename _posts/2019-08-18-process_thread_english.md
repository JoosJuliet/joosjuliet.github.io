---
layout: post
section-type: post
title: "Process vs Thread"
category: OS
tags: [ 'OS' ]
comments: true
---

# Process vs Thread

The primary difference is that threads within the same process run in a shared memory space excepted stack section, while processes run in separate memory spaces.

A process assign separated code, data, heap, stack section. but thread only assign separated stack section. so thread have some advantages. Especially they share heap section, they can fast resource sharing and effective utilization of multithread. But they have some side-effects. They are synchronization and deadlock.

So if we use multithread, we must consider problem of side-effects. But they have so much hard time to debugging. Because if one thread have problem, The whole process is affected.

---

reference:
https://www.geeksforgeeks.org/thread-in-operating-system/
