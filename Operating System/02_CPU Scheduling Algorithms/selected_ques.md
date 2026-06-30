# CPU Scheduling Question

## Question

The sequence **.......** is an optimal **non-preemptive** scheduling sequence for the following jobs which leaves the CPU idle for **.....** unit(s) of time.

| PID | Arrival Time | Burst Time |
|-----|-------------:|-----------:|
| 1 | 0.0 | 9 |
| 2 | 0.6 | 5 |
| 3 | 1.0 | 1 |

### Options

- (A) {3,2,1}, 1
- (B) {2,1,3}, 0
- (C) {3,2,1}, 0
- (D) {1,2,3}, 5

---

## Answer

✅ **Correct Option: (A) {3,2,1}, 1**

### Explanation

Since the scheduler is **non-preemptive**, it can choose to keep the CPU idle initially to obtain a better overall schedule.

- At **t = 0**, only **P1** has arrived.
- If the scheduler waits until **t = 1**, all three processes are available.
- It then executes the jobs in **Shortest Job First (SJF)** order:

| Process | Start | Finish |
|---------|------:|-------:|
| Idle | 0 | 1 |
| P3 | 1 | 2 |
| P2 | 2 | 7 |
| P1 | 7 | 16 |

- CPU remains idle for **1 unit** (from **0 to 1**).

Therefore,

- **Scheduling sequence:** `{3,2,1}`
- **CPU idle time:** `1 unit`

**Answer: (A)**