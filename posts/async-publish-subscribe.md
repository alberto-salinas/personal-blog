---
title: "A bare bone implementation of publish and subscribe using Python"
date: "2021-01-05"
---

Imagine you are still in a pandemic and would like to build a service that publishes
some cool sci-fi recomendations. I thought of reinventing the wheel and build my own
pub/sub where I simulate a queue where subscribers get a sci-fi film.

```python

from threading import Thread
from queue import Queue
from time import sleep

def consumer(in_queue):
    while True:
        movieToWatchDuringPandemic = in_queue.get()
        print(movieToWatchDuringPandemic)
        in_queue.task_done()

def producer(out_queue):
    producedElements = ['Blade Runner', 'Solaris', 'Ex Machina']
    while producedElements:
        # produce some cool data field
        data = producedElements.pop()
        out_queue.put(data)
        sleep(4)


production_queue = Queue()

t1 = Thread(target=consumer, args=(production_queue,))
t2 = Thread(target=producer, args=(production_queue,))

t1.start()
t2.start()
```
