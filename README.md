# Kernel Task Viewer Module

Welcome to the **Kernel Task Viewer Module**, a Linux kernel module designed to list and display all currently running tasks in the system. This project dynamically traverses the process tree, starting from the initial process (`init`), and logs vital information about every active task.

## Overview

This project demonstrates how to interact with the Linux kernel to retrieve and display task information, such as the **Process ID (PID)**, **Process State**, **Parent PID**, and **Task Name**. The module creates a structured process tree starting from the `init` process, providing a snapshot of the system's tasks in real-time.

The core functionality is implemented in the C file `CS345.c`, which integrates directly with the Linux kernel, and is compiled using the accompanying `Makefile`.

## Features

- **Dynamic Task Tree Traversal**: The module starts with the `init` process and recursively lists all child and sibling tasks.
- **Detailed Process Information**: For each task, it logs the **State**, **PID**, **Parent’s PID**, and **Task Name**.
- **Real-Time Kernel Logging**: Task information is output to the kernel logs using `printk()`, viewable through `dmesg`.
- **Modular and Clean**: The module is easy to load, unload, and manage within the Linux kernel.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Installation](#installation)
3. [Usage](#usage)
4. [Module Functions](#module-functions)
5. [Sample Output](#sample-output)

## Getting Started

To build and run this module, you need a Linux environment with kernel module support enabled. Familiarity with basic Linux commands and kernel module management is also recommended.

### Prerequisites

- Linux OS (with kernel development tools installed)
- GNU Compiler Collection (GCC)
- Root access (for inserting and removing kernel modules)

### Files

- **CS345.c**: Main C file containing the kernel module logic.
- **Makefile**: Instructions to compile and manage the module.

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/Kernel-Task-Viewer.git
    cd Kernel-Task-Viewer
    ```

2. Compile the module:
    ```bash
    make
    ```

3. Insert the compiled module into the kernel:
    ```bash
    sudo insmod CS345.ko
    ```

4. Verify the module insertion:
    ```bash
    lsmod | grep CS345
    ```

## Usage

Once the module is loaded, it starts by traversing the system's process tree from the `init` process, recursively listing all active tasks. You can view the logged output using `dmesg`.

### Commands

- **Compile the module**:
    ```bash
    make
    ```
  
- **Insert the module into the kernel**:
    ```bash
    sudo insmod CS345.ko
    ```

- **View the process information**:
    ```bash
    dmesg
    ```

- **Remove the module from the kernel**:
    ```bash
    sudo rmmod CS345.ko
    ```

- **Verify module removal**:
    ```bash
    lsmod | grep CS345
    ```

## Module Functions

- **mod_init()**: Initializes the kernel module, starting from the `init` process, and sets up the task traversal.
- **tree_proc()**: Recursively traverses the task tree, logging the state, PID, parent PID, and task name.
- **mod_exit()**: Handles cleanup when the module is removed from the kernel.

## Sample Output

After loading the module, you can use `dmesg` to view the output:

```bash
[ 1234.5678 ] Task Name: systemd, PID: 1, Parent PID: 0, State: Running
[ 1234.5679 ] Task Name: bash, PID: 2345, Parent PID: 1, State: Sleeping
[ 1234.5680 ] Task Name: sshd, PID: 6789, Parent PID: 2345, State: Running
...
```

The output will show the state of every process, its PID, its parent PID, and its name.

---

### Author

*Developed by [Rohan Chandrashekar]*  

---

## Contributing

Contributions are welcome! If you'd like to contribute, feel free to fork the repository and submit a pull request with your changes.

---
