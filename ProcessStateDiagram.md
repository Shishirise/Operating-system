# Operating Systems Concepts Summary

## System Calls and Processes

-   **System Calls**: Interface between user programs and the OS kernel
    (e.g., `read`, `write`, `fork`, `exec`, `wait`).
-   **File Descriptors**: Standard streams (0: stdin, 1: stdout, 2:
    stderr).
-   **File Management Calls**: `open`, `read`, `write`, `lseek`,
    `close`, with permissions and flags.
-   **Process Management Calls**: `fork`, `exec`, `wait`, `exit`,
    `getpid`, `getppid`.

## Fork and Process Behavior

-   `fork()` duplicates a process into **parent** and **child**.
-   Parent sees `pid > 0` (child PID), child sees `pid == 0`.
-   Output before `fork()` runs **once** (only parent).
-   Output after `fork()` may run **twice** (both parent and child).
-   Example explored: which process prints `"I am the parent..."` vs
    `"I am the child..."`.

## Process and Threads

-   **Process**: An independent program in execution (own memory, PC,
    registers).
-   **Thread**: Lightweight unit of execution inside a process, sharing
    memory/resources.
-   **Multiprogramming**: CPU switches between processes to maximize
    utilization.
-   **Process Model**: Conceptual view of multiple sequential processes
    running concurrently.

## Process State Diagram

-   States: **New**, **Ready**, **Running**, **Waiting/Blocked**,
    **Terminated**.
-   Transitions:
    -   New → Ready (admitted).
    -   Ready → Running (scheduler dispatch).
    -   Running → Waiting (I/O request).
    -   Waiting → Ready (I/O completion).
    -   Running → Terminated (exit).
    -   Running → Ready (interrupt/preemption).
-   Example: A process needing keyboard input goes New → Ready → Running
    → Waiting → Ready → Running → Terminated.


```text
   +-----+        +-------+
   | New | -----> | Ready |
   +-----+        +-------+
                     |
                     v
                  +--------+
                  | Running|
                  +--------+
                 /          \\
       (I/O wait)/            \\(Time slice over / interrupt)
               v                v
          +---------+        +-------+
          | Waiting |------> | Ready |
          +---------+        +-------+
                  \\
                   v
              +-----------+
              | Terminated|
              +-----------+
```




## Key Questions Discussed

1.  How many times does `"Start of program"` print in a fork example?
    (Once, before fork.)
2.  Can a process be in more than one state? (No, though threads of a
    process can.)
3.  On an n-processor system, how many processes can be in Running state
    at once? (At most `n`).

------------------------------------------------------------------------
