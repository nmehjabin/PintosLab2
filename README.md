# Pintos Project 2 — User Programs

Implementation of system call handling, user program loading, process management, and argument passing for the Pintos teaching operating system.

# Overview

This project extends the Pintos kernel to correctly execute user programs, handle system calls, manage process hierarchies, and safely interact with user memory.
Work is implemented inside src/userprog/ and integrates with other parts of the Pintos codebase (threads/, filesys/, etc.).

The main goals of Pintos Project 2 are:

- Add system calls (exit, exec, wait, read, write, file ops, etc.)

- Properly load ELF executables and pass arguments

- Create and manage processes and parent-child relationships

- Implement basic file descriptor tables for each process

- Enforce memory safety between kernel and user space

# Repository Structure
<img width="655" height="296" alt="Screenshot 2025-11-24 at 12 09 27 PM" src="https://github.com/user-attachments/assets/4b5e5b5f-9d61-458d-8714-71cd9799766d" />



# How to Build & Run

These steps assume Pintos is set up on Linux with PATH variables configured.

Build:
cd src/userprog
make

Run a user program:
pintos --filesys-size=2 -- -q run 'echo x'

Run all tests:
make check

To view a specific test’s output:
pintos -v -- -q run 'test-name'


# Key Design Decisions 

Memory Safety: All system call arguments are validated using a custom check_user_ptr() function that ensures pointers lie in user space and are mapped in the page directory.

Synchronization: Child/parent process synchronization uses semaphores (sema_down, sema_up) to block parents until children finish loading or exiting.

File System: A per-process lock prevents race conditions when multiple processes access the file system.
