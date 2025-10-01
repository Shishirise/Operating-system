```C++
//Shishir Adhikari
//COMPS 4103
//Mini Project 1: This program creates three child processes using fork()
//Each child process prints a specific range of numbers.
//The parent process waits for all child processes to complete before printing "Goodbye".

//Include necessary headers
#include <iostream> // For input and output
#include <unistd.h> // For fork() 
#include <sys/wait.h> // For waiting on child processes

int main() {

    // pid variable to store process ID
    pid_t pid;

    // First child process
    // create new process for first child
    pid = fork();
    if(pid == 0) {
        //loop to print numbers from 100 to 120
        for(int i = 100; i <= 120; i++) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
        return 0;
    }

    // Second child process
    // create new process for second child
    pid = fork();
    if(pid == 0) {
        //loop to print numbers from 200 to 220
        for(int i = 200; i <= 220; i++) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
        return 0;
    }

    // Third child process
    // create new process for third child
    pid = fork();
    if(pid == 0) {
        //loop to print numbers from 300 to 320
        for(int i = 300; i <= 320; i++) {
            std::cout << i << " ";
        }
        std::cout << std::endl;
        return 0;
    }

    // Parent waits for all children
    for(int i = 0; i < 3; i++) {
        // wait for any child process to finish
        waitpid(-1, NULL, 0);
    }

    // Print goodbye message
    std::cout << "Goodbye" << std::endl;
    return 0;
}

```
