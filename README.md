# Threadpool
Threadpool for multi-uses in C.
Creator: Moeen Abu Katish

<<Introduction>>
This project is a multi-threaded thread pool implementation in C, providing a framework for managing and executing asynchronous tasks efficiently. The thread pool allows users to submit tasks for execution, which are then processed by a pool of worker threads. This README provides an overview of the features, usage, and design of the thread pool implementation.


<<Functionality Overview>>

==create_threadpool(int num_threads_in_pool)==

Creates a thread pool with the specified number of worker threads.
Initializes synchronization primitives and data structures.
Returns a pointer to the created thread pool.

==enqueue(threadpool from_me, work_t work)==

Enqueues a new task into the thread pool's task queue.
Handles insertion of tasks into the queue in a thread-safe manner.

==dispatch(threadpool from_me, dispatch_fn dispatch_to_here, void arg)==

Dispatches a new task for asynchronous execution by the thread pool.
Associates the task function and its arguments with a work_t structure.
Enqueues the task into the thread pool for execution.

==do_work(void p)==

Worker thread function that continuously waits for tasks to execute.
Dequeues tasks from the thread pool's task queue and executes them.
Handles thread synchronization to ensure mutual exclusion.

==dequeue(threadpool tp)==

Removes and returns the next task from the thread pool's task queue.
Handles dequeuing of tasks from the queue in a thread-safe manner.
Adjusts the queue pointers and size accordingly.

==destroy_threadpool(threadpool destroyme)==

Initiates the destruction process of the thread pool.
Prevents the acceptance of new tasks and waits for ongoing tasks to complete.
Signals worker threads to exit gracefully and cleans up resources.

==Task(void arg)==

Example task function that represents the work to be done by worker threads.
Can be replaced with custom task functions depending on the application's requirements.

<<Features>>

Dynamically allocates and manages a pool of threads.
Enqueues tasks for asynchronous execution by worker threads.
Supports concurrent execution of multiple tasks.
Provides thread safety through mutex and conditional variable synchronization.
Gracefully handles shutdown and destruction of the thread pool.
Thread Pool Overview:
The thread pool implementation consists of the following components and functionalities:

<<Threadpool Creation>>

Creates a thread pool with a specified number of worker threads.
Initializes mutex and conditional variables for synchronization.

<<Task Enqueueing>>

Allows users to enqueue tasks for asynchronous execution.
Ensures thread safety during task enqueueing operations.
Task Execution:

Worker threads continuously wait for tasks to be enqueued.
Upon receiving a task, a worker thread dequeues and executes it.

<<Threadpool Destruction>>

Gracefully shuts down the thread pool upon destruction.
Waits for ongoing tasks to complete before terminating worker threads.

<<Error Handling>>

Provides error messages for failed operations, such as memory allocation and thread creation.

To use the thread pool implementation in a project, follow these steps:

Include the "threadpool.h" header file in your source code.
Create a thread pool using the create_threadpool function, specifying the desired number of threads.
Enqueue tasks for execution using the dispatch function, providing the task function and arguments.
Destroy the thread pool using the destroy_threadpool function when no longer needed.

Below is an example usage of the thread pool implementation:

gcc -Wall -o threadpool threadpool.c -lpthread

This command compiles the threadpool.c source file into an executable named threadpool, linking it with the pthread library for thread support.

Once compiled, you can run the program with the desired arguments. Here's an example usage:

./threadpool 5 10 15


<<In this command>>:

5 represents the size of the thread pool, indicating that there will be 5 worker threads in the pool.
10 represents the number of tasks to be dispatched to the thread pool.
15 represents the maximum number of tasks to be processed by the thread pool. If the number of dispatched tasks exceeds this limit, they won't be processed.
Adjust the arguments as needed based on your requirements. After execution, the program will create a thread pool with 5 worker threads, dispatch 10 tasks for execution, and limit the maximum number of tasks to 15.
