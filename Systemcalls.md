# POSIX System Calls Cheat Sheet

## 1. File Management System Calls

| Return Code | System Call 
|-------------|------------|
| fd = open(filename, flags, mode) | Open a file and return a file descriptor |
| fd = creat(filename, mode) | Create a new file with given permissions |
| s = close(fd) | Close an open file descriptor |
| n = read(fd, buffer, nbytes) | Read nbytes from file into buffer |
| n = write(fd, buffer, nbytes) | Write nbytes from buffer to file |
| position = lseek(fd, offset, whence) | Move file pointer (SEEK_SET, SEEK_CUR, SEEK_END) |
| s = stat(filename, &buf) | Get file metadata |
| s = fstat(fd, &buf) | Get metadata of open file descriptor |
| s = chmod(filename, mode) | Change file permissions |
| s = chown(filename, owner, group) | Change file owner/group |
| s = unlink(filename) | Delete a file |
| s = mkdir(dirname, mode) | Create a directory |
| s = rmdir(dirname) | Remove a directory |
| s = chdir(dirname) | Change current working directory |
| cwd = getcwd(buffer, size) | Get current working directory |
| s = link(oldname, newname) | Create a hard link |
| s = symlink(target, linkname) | Create a symbolic link |
| n = readlink(linkname, buffer, size) | Read symbolic link target |
| s = truncate(filename, length) / ftruncate(fd, length) | Change file size |

## 2. Process Control System Calls

| Return Code | System Call 
|-------------|------------|
| p = fork() | Create a new process (child) |
| s = execv(program, argv) | Replace current process image with a new program |
| s = wait(&status) | Wait for child process to terminate |
| s = waitpid(pid, &status, options) | Wait for a specific child process |
| s = exit(status) | Terminate current process |
| pid = getpid() | Get current process ID |
| ppid = getppid() | Get parent process ID |
| uid = getuid() / euid = geteuid() | Get user ID / effective user ID |
| s = setuid(uid) / s = seteuid(uid) | Set user ID / effective user ID |
| s = kill(pid, signal) | Send signal to a process |
| s = sleep(seconds) | Suspend process for a time |
| s = alarm(seconds) | Set a timer to send SIGALRM |

## 3. Directory & File System System Calls

| Return Code | System Call | 
|-------------|------------|
| s = opendir(dirname) | Open a directory stream |
| entry = readdir(dir) | Read an entry from directory stream |
| s = closedir(dir) | Close directory stream |
| s = mount(source, target, fstype, flags, data) | Mount a filesystem |
| s = umount(target) | Unmount a filesystem |
| s = mknod(filename, mode, dev) | Create a special file (device) |

## 4. Device & File Descriptor Control

| Return Code | System Call |
|-------------|------------|
| fd2 = dup(fd) | Duplicate a file descriptor |
| fd2 = dup2(fd, fd2) | Duplicate a file descriptor to a specific number |
| s = fcntl(fd, command, arg) | Perform file descriptor operations (locking, flags) |
| s = ioctl(fd, request, arg) | Device-specific I/O control operations |
| s = pipe(fds) | Create a pipe for inter-process communication |

## 5. Memory & System Information

| Return Code | System Call |
|-------------|------------|
| s = brk(addr) / sbrk(nbytes) | Adjust process data segment size |
| addr = mmap(addr, length, prot, flags, fd, offset) | Map file or device into memory |
| s = munmap(addr, length) | Unmap memory region |
| time = gettimeofday(&tv, NULL) | Get current system time |
| s = uname(&buf) | Get system information (OS name, version, architecture) |

---

**Notes:**
- Most system calls return **-1** on error.
- Include headers: `<unistd.h>`, `<fcntl.h>`, `<sys/stat.h>`, `<sys/types.h>`, `<sys/mount.h>`
- These are **POSIX-compliant system calls**, used in **C on UNIX/Linux**.

