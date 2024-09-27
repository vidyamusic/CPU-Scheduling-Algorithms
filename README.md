# CPU-Scheduling-Algorithms

An implementation of various CPU scheduling algorithms in C++, including First Come First Serve (FCFS), Round Robin (RR), Shortest Process Next (SPN), Shortest Remaining Time (SRT), Highest Response Ratio Next (HRRN), Feedback (FB), and Aging.

## Table of Contents

- [CPU-Scheduling-Algorithms](#cpu-scheduling-algorithms)
  - [Algorithms](#algorithms)
    - [First Come First Serve (FCFS)](#first-come-first-serve-fcfs)
    - [Round Robin with varying time quantum (RR)](#round-robin-with-varying-time-quantum-rr)
    - [Shortest Process Next (SPN)](#shortest-process-next-spn)
    - [Shortest Remaining Time (SRT)](#shortest-remaining-time-srt)
    - [Highest Response Ratio Next (HRRN)](#highest-response-ratio-next-hrrn)
    - [Feedback (FB)](#feedback-fb)
    - [Feedback with varying time quantum (FBV)](#feedback-with-varying-time-quantum-fbv)
    - [Aging](#aging)
  - [Installation](#installation)
  - [Input Format](#input-format)
  - [Contributors](#contributors)

## Algorithms

### First Come First Serve (FCFS)

- First Come First Serve (FCFS) is a non-preemptive scheduling algorithm where the process that arrives first is executed first. It is straightforward to implement but can cause performance issues, such as the “convoy effect,” where long processes delay shorter ones. FCFS does not prioritize based on burst time or priority, making it suitable for batch systems where process order is critical.

### Round Robin with varying time quantum (RR)

- Round Robin (RR) with variable quantum dynamically adjusts the time slice allocated to each process, allowing for better handling of processes with different burst times.

- Each process is given a time slice to execute, and when its quantum expires, it is moved to the end of the queue, ensuring all processes receive CPU time.

- This adaptability reduces average waiting time and context-switching overhead, while also preventing starvation.

### Shortest Process Next (SPN)

- Shortest Process Next (SPN) is a non-preemptive scheduling algorithm that selects the process with the shortest burst time for execution, reducing average waiting time.

- Processes are sorted in a queue based on their burst times, with the shortest at the front. Once a process starts executing, it runs to completion.

- SPN minimizes waiting time for shorter processes but may cause longer processes to experience delays, leading to potential inefficiencies in overall system performance.

### Shortest Remaining Time (SRT)

- Shortest Remaining Time Next (SRT) is a preemptive scheduling algorithm that interrupts an executing process if a new process arrives with a shorter remaining time.

- It maintains a queue where processes are sorted based on their remaining time, ensuring that the one with the shortest time is executed first.

- SRT is advantageous for minimizing average waiting time, especially when burst times are unknown, as it dynamically adapts to changes in remaining times during execution.

### Highest Response Ratio Next (HRRN)

- Highest Response Ratio Next (HRRN) is a non-preemptive scheduling algorithm that prioritizes processes based on their response ratio, calculated as the ratio of waiting time to burst time.

- Processes are sorted in a queue according to their response ratio, ensuring the one with the highest ratio is executed first.

- HRRN is effective for minimizing average waiting time, especially when burst times are unknown, as it adapts to changes in waiting times during execution.

### Feedback (FB)

- Feedback is a multi-level priority scheduling algorithm that allocates CPU time based on process priority levels, employing multiple priority queues.

- Higher-priority processes are executed first, while new processes are added to the appropriate queue based on their priority. Upon completion, a process is demoted to the next lower priority queue.

- This algorithm effectively manages a diverse workload, ensuring that both high-priority and lower-priority processes are executed in a balanced manner, accommodating varying execution times and priorities.

### Feedback with varying time quantum (FBV)

- Same as [Feedback](#feedback-fb) but with varying time quantum.
- Feedback with varying time quantum also uses multiple priority queues and assigns a different time quantum for each priority level, it allows the algorithm to be more efficient by spending more time on higher-priority processes and less time on lower-priority processes.

### Aging

- Xinu is an operating system developed at Purdue University that implements a scheduling invariant ensuring that the highest priority process eligible for CPU service is always executing, utilizing round-robin scheduling among processes with equal priority. This policy can lead to starvation for lower-priority processes, as they may be perpetually preempted by higher-priority ones. The set of processes in the ready list and the currently executing process are collectively referred to as eligible processes.

- To mitigate starvation, an aging scheduler can be implemented. During each rescheduling event, such as a timeout, the scheduler increments the priority of all ready processes by a fixed amount. This mechanism ensures that each ready process can only be bypassed a limited number of times before acquiring the highest priority.

- Each process is assigned an initial priority at creation. Upon each invocation of the scheduler, the following steps are executed:

- The current process's priority is reset to its initial value. The priorities of all ready processes (excluding the current process) are incremented by one.

- The scheduler selects the highest priority process from the pool of eligible processes.
  It is important to note that the complete ready list must be traversed during each scheduler invocation.

## Installation

1- Clone the repository

2- Install g++ compiler and make

```bash
sudo apt-get install g++ make
```

3- Compile the code using `make` command

4- Run the executable file

## Input Format

- Line 1: "trace" or "stats" to specify the type of output desired

- Line 2: a comma-separated list of CPU scheduling policies to analyze/visualize, including relevant parameters if applicable. Each algorithm is denoted by a number as outlined in the introduction section and demonstrated in the accompanying test cases. For example, Round Robin and Aging policies require a quantum parameter q. Hence, a policy formatted as 2-4 signifies Round Robin with 𝑞=4, while 8-1 indicates Aging with 𝑞=1.

1.  FCFS (First Come First Serve)
2.  RR (Round Robin)
3.  SPN (Shortest Process Next)
4.  SRT (Shortest Remaining Time)
5.  HRRN (Highest Response Ratio Next)
6.  FB-1, (Feedback where all queues have q=1)
7.  FB-2i, (Feedback where q= 2i)
8.  Aging

- Line 3: Specify an integer representing the last time instant to be utilized in simulation and displayed on timeline.

- Line 4: Indicate and integer for number of processes to be stimulated.

- Line 5: Begin the description of processes. Each process should be described on a new line. For algorithms 1 through 7, each process is characterized by a comma-separated list containing:

  1- String specifying a process name\
   2- Arrival Time\
   3- Service Time

- **Note:**

For the Aging algorithm (Algorithm 8), each process is defined using a comma-separated list comprising:

A string denoting the process name
Arrival Time
Priority
Processes should be sorted according to their arrival time. In cases where two processes share the same arrival time, the process with the lower priority is considered to arrive first.

Refer to the attached testcases (https://github.com/yousefkotp/CPU-Scheduling-Algorithms/tree/main/testcases) for additional details.
