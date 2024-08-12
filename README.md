# xv6

> xv6 is a re-implementation of Dennis Ritchie's and Ken Thompson's Unix Version 6 (v6). xv6 loosely follows the structure and style of v6, but is implemented for a modern x86-based multiprocessor using ANSI C.

## Implementing Shell Commands in xv6

### Introduction
Implementing and modifying Unix-like shell commands in the xv6 operating system.

### Modified ls Command
**Feature Enhancements:**
- **Automatic Hiding of Hidden Files and Directories:** By default, the `ls` command omits hidden files and directories (those prefixed with a `.`), reducing clutter from system and configuration files.
- **Directory Differentiation:** Directory names now have a trailing slash (`/`), allowing users to easily distinguish them from regular files.
- **Introduction of the `-a` Flag:** The new `-a` flag shows all files, including hidden ones, providing a complete directory view when needed.

**Files to Edit:** `ls.c`, `Makefile`

### Implementing the sleep Command
**Implementation Details:** Implement the UNIX program `sleep` for xv6. The `sleep` command pauses for a user-specified number of ticks. The implementation should handle invalid inputs by printing an error message.

**Files to Edit:** `sleep.c`, `Makefile`

### Implementing the uniq Command
**Implementation Details:** The `uniq` command filters out adjacent duplicate lines from the input file and writes the filtered data to the output. Additionally, implement the following flags:
- `-c`: Prefix lines by the number of occurrences
- `-i`: Ignore differences in case when comparing
- `-d`: Only print duplicate lines

**Files to Edit:** `uniq.c`, `Makefile`

### Implementing the find Command
**Implementation Details:** The `find` command searches for files in a directory hierarchy. Implement the following features:
- Default find functionality: `find <folder> -name <name>`
- `-type` flag with `f` (files) and `d` (directories)
- `-size` flag with exact, greater than, and less than byte sizes

**Files to Edit:** `find.c`, `Makefile`

## Syscalls and Schedulers

### Adding time_scheduled Syscall
**Implementation Details:** Implement the `time_scheduled(pid)` system call to track how many ticks each process has been scheduled. Return 0 for unscheduled processes and -1 for non-existent processes.

**Files to Edit:** `sysproc.c`, `user.h`, `usys.S`, `Makefile`

### Implementing a Basic Scheduler
**Scheduler Options:**
- FIFO: First-in, first-out
- SJF: Shortest job first
- RR: Round-robin
- Stride: Stride scheduling

**Files to Edit:** `proc.c`, `proc.h`, `Makefile`

### Implemented a More Interesting Scheduler
**Scheduler Options:**
- Lottery: Implement lottery scheduling with a syscall to set and get ticket counts
- Priority: Support at least 3 priority levels with FIFO, SJF, or RR within each level
- STCF: Shortest time to completion first using exponential averaging for job size

**Files to Edit:** `proc.c`, `proc.h`, `Makefile`

### Performance Analysis
Compare the new schedulers against the default scheduler using `time_scheduled()` and `uptime()`. Analyze performance for the following commands:
- `stressfs`
- `uniq`
- `find`
- `cat README | uniq`

## Virtual Memory

### Understanding sbrk()
**Task Details:** Modify `sbrk()` to remove page allocation, causing it to only increment the process size. Analyze what breaks and explain why.

**Files to Edit:** `sysproc.c`

### Implementing Lazy Allocation
**Task Details:** Implement lazy page allocation by handling page faults in `trap.c`. Ensure simple commands like `echo`, `ls`, `cat`, `wc`, and `mkdir` work correctly.

**Files to Edit:** `trap.c`, `vm.c`

### Evaluating and Explaining Lazy Allocation
**Task Details:** Add print statements in page fault handling code and take screenshots of basic commands. Explain the implementation and how the screenshots demonstrate correct behavior.

## File Systems

### Adding lseek Support
**Task Details:** Implement the `lseek` system call and modify `filewrite` to handle holes in files.

**Files to Edit:** `file.c`, `file.h`

### Implement the symlink(target, path) system call to create symbolic links and modify open to handle them.

**Files to Edit:** `syscall.c`, `sysfile.c`, `file.h`, `stat.h`

### Supporting Large Files
**Task Details:** Modify the file system to support doubly-indirect blocks, allowing files up to 16,523 blocks in size.

**Files to Edit:** `fs.c`, `fs.h`

### Implementing Extent-Based Files
**Task Details:** Modify the inode structure to support extent-based files and demonstrate their functionality using a user program.

**Files to Edit:** `fs.c`, `fs.h`, `file.c`, `file.h`
