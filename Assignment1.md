<img width="1148" height="791" alt="image" src="https://github.com/user-attachments/assets/c9eea3df-a8f8-4e45-8f56-65220ad28f32" />


## Quantum and Processes

- **Quantum:** 0.25 s  
- **Processes and Burst Times:**

| Process | Burst Time (s) | Number of Slices (0.25 s each) |
|---------|----------------|--------------------------------|
| P0      | 5              | 20                             |
| P1      | 2              | 8                              |
| P2      | 4              | 16                             |
| P3      | 3              | 12                             |
| P4      | 6              | 24                             |

- **Order of Arrival:** P0 → P1 → P2 → P3 → P4  
- Each process is removed from the queue once it **finishes execution**.


## How Round-Robin Works

### Each process is divided into quanta
- Here, **quantum = 0.25 s**, so each “time slot” is 0.25 s.  
- A process may need **multiple quanta** to finish its total burst time.  

### Slices
- Each 0.25 s execution of a process is called a **slice**.  
- **Number of slices = Burst time ÷ Quantum**.  

### Completion Time
- A process’s **completion time** is when its **last slice finishes**.  

### Termination
- After a process completes all its slices, it is **removed from the ready queue** and no longer scheduled.  

### Remaining Processes
- The CPU continues rotating among the **unfinished processes** in the original RR order (P0 → P1 → P2 → P3 → P4).  
- This repeats until **all processes finish**.

---

## Notes

- The timeline for CPU execution can show **multiple entries** for the same process if it is not finished in one quantum.  
- For example, P0 with 20 slices will appear **20 times in the timeline**, once per quantum until completion.  


## Gantt chart slice by slice
```txt
0.00 - 0.25   [P0]  (slice 1)
0.25 - 0.50   [P1]  (slice 1)
0.50 - 0.75   [P2]  (slice 1)
0.75 - 1.00   [P3]  (slice 1)
1.00 - 1.25   [P4]  (slice 1)

1.25 - 1.50   [P0]  (slice 2)
1.50 - 1.75   [P1]  (slice 2)
1.75 - 2.00   [P2]  (slice 2)
2.00 - 2.25   [P3]  (slice 2)
2.25 - 2.50   [P4]  (slice 2)

2.50 - 2.75   [P0]  (slice 3)
2.75 - 3.00   [P1]  (slice 3)
3.00 - 3.25   [P2]  (slice 3)
3.25 - 3.50   [P3]  (slice 3)
3.50 - 3.75   [P4]  (slice 3)

3.75 - 4.00   [P0]  (slice 4)
4.00 - 4.25   [P1]  (slice 4)
4.25 - 4.50   [P2]  (slice 4)
4.50 - 4.75   [P3]  (slice 4)
4.75 - 5.00   [P4]  (slice 4)

5.00 - 5.25   [P0]  (slice 5)
5.25 - 5.50   [P1]  (slice 5)
5.50 - 5.75   [P2]  (slice 5)
5.75 - 6.00   [P3]  (slice 5)
6.00 - 6.25   [P4]  (slice 5)

6.25 - 6.50   [P0]  (slice 6)
6.50 - 6.75   [P1]  (slice 6)
6.75 - 7.00   [P2]  (slice 6)
7.00 - 7.25   [P3]  (slice 6)
7.25 - 7.50   [P4]  (slice 6)

7.50 - 7.75   [P0]  (slice 7)
7.75 - 8.00   [P1]  (slice 7)
8.00 - 8.25   [P2]  (slice 7)
8.25 - 8.50   [P3]  (slice 7)
8.50 - 8.75   [P4]  (slice 7)

8.75 - 9.00   [P0]  (slice 8)
9.00 - 9.25   [P1]  (slice 8)  ← P1 finishes here (2 s total)
9.25 - 9.50   [P2]  (slice 8)
9.50 - 9.75   [P3]  (slice 8)
9.75 - 10.00  [P4]  (slice 8)

10.00 - 10.25 [P0]  (slice 9)
10.25 - 10.50 [P2]  (slice 9)
10.50 - 10.75 [P3]  (slice 9)
10.75 - 11.00 [P4]  (slice 9)

11.00 - 11.25 [P0]  (slice 10)
11.25 - 11.50 [P2]  (slice 10)
11.50 - 11.75 [P3]  (slice 10)
11.75 - 12.00 [P4]  (slice 10)

12.00 - 12.25 [P0]  (slice 11)
12.25 - 12.50 [P2]  (slice 11)
12.50 - 12.75 [P3]  (slice 11)
12.75 - 13.00 [P4]  (slice 11)

13.00 - 13.25 [P0]  (slice 12)
13.25 - 13.50 [P2]  (slice 12)
13.50 - 13.75 [P3]  (slice 12)  ← P3 finishes here (3 s total)
13.75 - 14.00 [P4]  (slice 12)

14.00 - 14.25 [P0]  (slice 13)
14.25 - 14.50 [P2]  (slice 13)
14.50 - 14.75 [P4]  (slice 13)

14.75 - 15.00 [P0]  (slice 14)
15.00 - 15.25 [P2]  (slice 14)
15.25 - 15.50 [P4]  (slice 14)

15.50 - 15.75 [P0]  (slice 15)
15.75 - 16.00 [P2]  (slice 15)
16.00 - 16.25 [P4]  (slice 15)

16.25 - 16.50 [P0]  (slice 16)
16.50 - 16.75 [P2]  (slice 16)  ← P2 finishes here (4 s total)
16.75 - 17.00 [P4]  (slice 16)

17.00 - 17.25 [P0]  (slice 17)
17.25 - 17.50 [P4]  (slice 17)

17.50 - 17.75 [P0]  (slice 18)
17.75 - 18.00 [P4]  (slice 18)

18.00 - 18.25 [P0]  (slice 19)
18.25 - 18.50 [P4]  (slice 19)

18.50 - 18.75 [P0]  (slice 20)  ← P0 finishes here (5 s total)
18.75 - 19.00 [P4]  (slice 20)

19.00 - 19.25 [P4]  (slice 21)
19.25 - 19.50 [P4]  (slice 22)
19.50 - 19.75 [P4]  (slice 23)
19.75 - 20.00 [P4]  (slice 24)  ← P4 finishes here (6 s total)
```
# b. Ans

## Given

**Process P1 burst:** 2 s  
**Quantum (time slice):** 100 ms = 0.1 s  
**OS overhead:** negligible  
**Round-Robin order:** P0 → P1 → P2 → P3 → P4  
**All processes arrive at time 0**  

**Question:** When will P1 complete?
= 9.70

## Step 1: Convert burst into number of slices

Slices needed for P1 = Burst ÷ Quantum = 2 ÷ 0.1 = 20 slices

```txt
0.00 - 0.10   [P0]  (slice 1)
0.10 - 0.20   [P1]  (slice 1)
0.20 - 0.30   [P2]  (slice 1)
0.30 - 0.40   [P3]  (slice 1)
0.40 - 0.50   [P4]  (slice 1)

0.50 - 0.60   [P0]  (slice 2)
0.60 - 0.70   [P1]  (slice 2)
0.70 - 0.80   [P2]  (slice 2)
0.80 - 0.90   [P3]  (slice 2)
0.90 - 1.00   [P4]  (slice 2)

1.00 - 1.10   [P0]  (slice 3)
1.10 - 1.20   [P1]  (slice 3)
1.20 - 1.30   [P2]  (slice 3)
1.30 - 1.40   [P3]  (slice 3)
1.40 - 1.50   [P4]  (slice 3)

1.50 - 1.60   [P0]  (slice 4)
1.60 - 1.70   [P1]  (slice 4)
1.70 - 1.80   [P2]  (slice 4)
1.80 - 1.90   [P3]  (slice 4)
1.90 - 2.00   [P4]  (slice 4)

2.00 - 2.10   [P0]  (slice 5)
2.10 - 2.20   [P1]  (slice 5)
2.20 - 2.30   [P2]  (slice 5)
2.30 - 2.40   [P3]  (slice 5)
2.40 - 2.50   [P4]  (slice 5)

2.50 - 2.60   [P0]  (slice 6)
2.60 - 2.70   [P1]  (slice 6)
2.70 - 2.80   [P2]  (slice 6)
2.80 - 2.90   [P3]  (slice 6)
2.90 - 3.00   [P4]  (slice 6)

3.00 - 3.10   [P0]  (slice 7)
3.10 - 3.20   [P1]  (slice 7)
3.20 - 3.30   [P2]  (slice 7)
3.30 - 3.40   [P3]  (slice 7)
3.40 - 3.50   [P4]  (slice 7)

3.50 - 3.60   [P0]  (slice 8)
3.60 - 3.70   [P1]  (slice 8)
3.70 - 3.80   [P2]  (slice 8)
3.80 - 3.90   [P3]  (slice 8)
3.90 - 4.00   [P4]  (slice 8)

4.00 - 4.10   [P0]  (slice 9)
4.10 - 4.20   [P1]  (slice 9)
4.20 - 4.30   [P2]  (slice 9)
4.30 - 4.40   [P3]  (slice 9)
4.40 - 4.50   [P4]  (slice 9)

4.50 - 4.60   [P0]  (slice 10)
4.60 - 4.70   [P1]  (slice 10)
4.70 - 4.80   [P2]  (slice 10)
4.80 - 4.90   [P3]  (slice 10)
4.90 - 5.00   [P4]  (slice 10)

5.00 - 5.10   [P0]  (slice 11)
5.10 - 5.20   [P1]  (slice 11)
5.20 - 5.30   [P2]  (slice 11)
5.30 - 5.40   [P3]  (slice 11)
5.40 - 5.50   [P4]  (slice 11)

5.50 - 5.60   [P0]  (slice 12)
5.60 - 5.70   [P1]  (slice 12)
5.70 - 5.80   [P2]  (slice 12)
5.80 - 5.90   [P3]  (slice 12)
5.90 - 6.00   [P4]  (slice 12)

6.00 - 6.10   [P0]  (slice 13)
6.10 - 6.20   [P1]  (slice 13)
6.20 - 6.30   [P2]  (slice 13)
6.30 - 6.40   [P3]  (slice 13)
6.40 - 6.50   [P4]  (slice 13)

6.50 - 6.60   [P0]  (slice 14)
6.60 - 6.70   [P1]  (slice 14)
6.70 - 6.80   [P2]  (slice 14)
6.80 - 6.90   [P3]  (slice 14)
6.90 - 7.00   [P4]  (slice 14)

7.00 - 7.10   [P0]  (slice 15)
7.10 - 7.20   [P1]  (slice 15)
7.20 - 7.30   [P2]  (slice 15)
7.30 - 7.40   [P3]  (slice 15)
7.40 - 7.50   [P4]  (slice 15)

7.50 - 7.60   [P0]  (slice 16)
7.60 - 7.70   [P1]  (slice 16)
7.70 - 7.80   [P2]  (slice 16)
7.80 - 7.90   [P3]  (slice 16)
7.90 - 8.00   [P4]  (slice 16)

8.00 - 8.10   [P0]  (slice 17)
8.10 - 8.20   [P1]  (slice 17)
8.20 - 8.30   [P2]  (slice 17)
8.30 - 8.40   [P3]  (slice 17)
8.40 - 8.50   [P4]  (slice 17)

8.50 - 8.60   [P0]  (slice 18)
8.60 - 8.70   [P1]  (slice 18)
8.70 - 8.80   [P2]  (slice 18)
8.80 - 8.90   [P3]  (slice 18)
8.90 - 9.00   [P4]  (slice 18)

9.00 - 9.10   [P0]  (slice 19)
9.10 - 9.20   [P1]  (slice 19)
9.20 - 9.30   [P2]  (slice 19)
9.30 - 9.40   [P3]  (slice 19)
9.40 - 9.50   [P4]  (slice 19)

9.50 - 9.60   [P0]  (slice 20)
9.60 - 9.70   [P1]  (slice 20)  ← **P1 finishes here (2 s total)**
9.70 - 9.80   [P2]  (slice 20)
9.80 - 9.90   [P3]  (slice 20)
9.90 - 10.00  [P4]  (slice 20)
```






