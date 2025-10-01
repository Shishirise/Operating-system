```C++
#include <iostream>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid;

    // First child
    pid = fork();
    if(pid == 0) {
        for(int i = 100; i <= 120; i++) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
        return 0;
    }

    // Second child
    pid = fork();
    if(pid == 0) {
        for(int i = 200; i <= 220; i++) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
        return 0;
    }

    // Third child
    pid = fork();
    if(pid == 0) {
        for(int i = 300; i <= 320; i++) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
        return 0;
    }

    // Parent waits for all children
    for(int i = 0; i < 3; i++) {
        waitpid(-1, NULL, 0);
    }

    std::cout << "Goodbye" << std::endl;
    return 0;
}
```
