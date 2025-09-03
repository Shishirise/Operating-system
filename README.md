# Operating-system

## System calls for process Management
```cpp
x = 3;
p = fork();   // create a new process
if (p == 0) {
    x = x + 1;   // only child does this
}
cout << x;
What happens:
Before fork:

x = 3

Only one process exists.

After p = fork();
Parent process: p > 0 → keeps x = 3
Child process: p == 0 → initially x = 3
Child process executes x = x + 1;
Child now has x = 4
Parent still has x = 3
Both processes execute cout << x;
Parent prints 3
Child prints 4

```
