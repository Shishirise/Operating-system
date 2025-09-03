# POSIX System Calls - Conditions and Real-World Usage

## 1. File Management System Calls

| System Call | Condition / When Used | Real-World Example |
|-------------|----------------------|------------------|
| open() | Access a file for reading/writing | Opening a configuration file to read settings |
| creat() | Create a new file | Creating a new log file for application events |
| close() | Finished with a file | Closing a file after reading data |
| read() | Read data from a file | Reading user data from a CSV file |
| write() | Write data to a file | Writing logs to a server log file |
| lseek() | Move file pointer for random access | Jumping to the middle of a binary file to update a record |
| stat() / fstat() | Check file info | Checking file size before reading into memory |
| chmod() | Change file permissions | Making a script executable (`chmod +x script.sh`) |
| chown() | Change file owner/group | Changing ownership of files on a shared server |
| unlink() | Delete a file | Deleting temporary files |
| mkdir() | Create a directory | Creating project folders in a build script |
| rmdir() | Remove an empty directory | Removing old empty log directories |
| chdir() | Change working directory | Switching to project folder before running scripts |
| getcwd() | Get current working directory | Displaying current directory in a shell prompt |
| link() | Create a hard link | Creating multiple references to the same file |
| symlink() | Create a symbolic link | Linking `/usr/bin/python3` to `/usr/bin/python` |
| readlink() | Read a symbolic link target | Resolving the real path behind a symlink |
| truncate() / ftruncate() | Change file size | Shortening log files to save space |

## 2. Process Control System Calls

| System Call | Condition / When Used | Real-World Example |
|-------------|----------------------|------------------|
| fork() | Create a new process | Web server creating child process to handle a request |
| execv() | Replace current process image | Running a script from a C program |
| wait() / waitpid() | Wait for child process | Parent waits for child to finish compiling |
| exit() | Terminate current process | Ending a program after completion |
| getpid() | Know current process ID | Logging process ID for debugging |
| getppid() | Know parent process ID | Child process communicating with parent |
| getuid() / geteuid() | Check user privileges | Program checking if user is root |
| setuid() / seteuid() | Change process privileges | Service dropping root privileges temporarily |
| kill() | Send a signal | Stopping a process (`kill -9 PID`) |
| sleep() | Pause execution | Waiting between network retries |
| alarm() | Set timer | Timing out long-running operations |

## 3. Directory & File System Calls

| System Call | Condition / When Used | Real-World Example |
|-------------|----------------------|------------------|
| opendir() / readdir() / closedir() | Reading directory contents | Listing all files in `/var/log/` for cleanup |
| mount() / umount() | Mount/unmount a filesystem | Mounting an external USB drive |
| mknod() | Create device or special files | Creating `/dev/ttyS1` for serial communication |

## 4. Device & File Descriptor Control

| System Call | Condition / When Used | Real-World Example |
|-------------|----------------------|------------------|
| dup() / dup2() | Redirect file descriptors | Redirect stdout to a log file |
| fcntl() | Locking or changing fd flags | Locking a file to prevent concurrent writes |
| ioctl() | Device-specific operations | Configuring network card parameters |
| pipe() | Inter-process communication | Parent process sending data to a child process |

## 5. Memory & System Info

| System Call | Condition / When Used | Real-World Example |
|-------------|----------------------|------------------|
| brk() / sbrk() | Adjust heap size manually | Rarely used; dynamic memory allocation internally uses this |
| mmap() / munmap() | Map files to memory | Loading large databases or shared memory between processes |
| gettimeofday() | Get precise system time | Logging timestamps for transactions |
| uname() | Get system info | Checking OS type/version in system monitoring tools |

---

**Summary:**
- File system calls: managing files, logs, configuration, directories
- Process control calls: multitasking, daemons, servers
- Device & FD control: I/O redirection, device communication, IPC
- Memory & info calls: shared memory, timing, system monitoring

