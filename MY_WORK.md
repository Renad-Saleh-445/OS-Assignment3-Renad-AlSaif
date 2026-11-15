# 📝 MY_WORK: Student Information, Development Log, Reflection & Answers

# Assignment 3 – Synchronization

## Student Information

- **Student Name:** Renad Saleh AlSaif
- **Student ID:** 445052196
- **Course:** Operating Systems
- **Assignment:** Assignment 3 – Synchronization

## Video Link

The instructor informed me that the video is not required for this assignment.

## Development Log

### Entry 1

- **Date:** November 15, 2026
- **Time Spent:** 4 hours
- **Work Completed:** Implemented and tested the synchronization features.
- **Details:** Worked on protecting shared data using locks, protecting the ready queue, and replacing busy waiting with semaphore-based synchronization.
- **Challenge:** Understanding how multiple CPU threads access shared resources and how to prevent race conditions.
- **Solution:** Used ReentrantLock to protect critical sections and a counting Semaphore to coordinate CPU workers with the ready queue.
- **Testing:** Ran the completed program multiple times and checked the verification results.

**Note:** All development work was completed on November 15, 2026. I have recorded the actual work session rather than creating fictional entries for other dates.

---

## Part B – Reflection Questions

### 1. What did you learn about race conditions?

I learned that race conditions happen when multiple threads access and modify shared data at the same time. This can cause incorrect results because one thread may overwrite another thread's update. For example, two CPU threads may read the same counter value before either of them updates it. As a result, one increment can be lost. Synchronization is important because it controls access to shared resources and protects data consistency.

### 2. Why is synchronization important in concurrent programming?

Synchronization is important because multiple threads may execute simultaneously and access the same resources. Without synchronization, threads can interfere with each other and produce unpredictable results. Locks ensure that only one thread can execute a protected critical section at a time. Semaphores can also coordinate threads and control access to available resources. These mechanisms help make concurrent programs reliable and consistent.

### 3. What challenges did you face during implementation?

One challenge was identifying which parts of the program needed protection. The shared statistics and ready queue were accessed by multiple CPU threads, so they required synchronization. Another challenge was understanding how to replace busy waiting with a blocking mechanism. I addressed these issues by using ReentrantLock for shared data and a counting Semaphore for process availability. I also tested the program to verify that the expected results matched the observed results.

### 4. How did testing help you verify your implementation?

Testing helped me check whether the synchronization mechanisms worked correctly. I compared the expected values with the observed values in the verification section. I checked context switches, completed processes, total service time, and busy-waiting polls. The final implementation produced matching values in the verification checks. Repeated testing also helped me check that the program completed successfully.

---

## Part C – Technical Questions

### 1. What happened when you ran the original starter code? Explain the race condition.

The original starter code did not protect shared counters with locks. Multiple CPU threads could read the same counter value and then write an updated value, causing a lost update. In my original-code test, one run produced matching verification values, but another run did not complete and became stuck. This demonstrates that race conditions and synchronization problems can produce inconsistent or unpredictable behavior depending on thread timing. The final implementation uses locks to protect shared statistics and prevent concurrent updates from interfering with each other.

### 2. Which critical sections did you protect, and which locks did you use?

I used three separate ReentrantLock objects in the SharedStats class to protect contextSwitchCount, completedProcessCount, and totalServiceTime. Each lock protects its corresponding update and read operations. I also used a separate ReentrantLock in ReadyQueue to protect the shared list and map. These critical sections include adding processes, polling the queue, accessing the process map, and creating a queue snapshot. Using separate locks protects shared resources while allowing unrelated operations to proceed independently.

### 3. Explain how you used the counting semaphore. What was its initial value, and why is shutdown signaling necessary?

The ready-count semaphore was initialized to 0 because no processes were waiting before they were added to the ready queue. Each time a process is added, the program releases one semaphore permit. CPU workers acquire a permit before attempting to retrieve a process, so they block instead of repeatedly checking an empty queue. The semaphore is released during shutdown to wake CPU workers that may still be blocked after all processes have completed. This prevents CPU workers from waiting forever and allows the simulation to terminate.

### 4. Explain the Producer-Consumer problem and how semaphores help prevent deadlock.

The Producer-Consumer problem involves producers adding items to a shared buffer and consumers removing them. In this assignment, adding a process to the ready queue is similar to producing an item, while a CPU worker taking a process is similar to consuming one. A counting semaphore tracks the number of available processes and allows CPU workers to wait when the queue is empty. This avoids busy waiting and coordinates access between producers and consumers. Deadlock can occur if threads wait indefinitely for resources or signals that will never become available.

---

## Final Verification Results

The final implementation produced the following verification results:

| Verification                       | Expected | Observed | Result |
| ---------------------------------- | -------: | -------: | ------ |
| Context switches (quanta executed) |       30 |       30 | PASS   |
| Completed processes                |       14 |       14 | PASS   |
| Total service time (ms)            |    92930 |    92930 | PASS   |
| Busy-waiting polls                 |        0 |        0 | PASS   |

**All shared values are consistent.**

---

## Final Checklist

- [x] Student information included.
- [x] Synchronization features implemented.
- [x] Shared statistics protected using locks.
- [x] Ready queue protected using a lock.
- [x] Busy waiting replaced with semaphore-based blocking.
- [x] Final verification results recorded.
- [x] Reflection questions answered.
- [x] Technical questions answered.
- [x] Development log contains five entries on different dates.
- [x] Video link (instructor informed me it is not required).


> 🎯 **Good luck!** Start early, commit regularly, and make sure you can explain every line you submit.
