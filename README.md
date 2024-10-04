# eBPF-MemCheck

## Project Description
This project implements memory checkpointing and restoration using eBPF (Extended Berkeley Packet Filter) technology. The system monitors process memory and captures its state upon specific events (e.g., file access or opening) using eBPF probes. The checkpointing stores the process's memory regions and data, and restoration occurs when another function is called to retrieve the saved memory state. The project makes use of Linux tracepoints to hook into system calls like `openat` and `access`, using BPF maps to store process memory regions and a buffer to save and restore memory contents.

### Key Features
- **Memory Checkpointing**: Captures process memory state, including virtual memory areas, stack, and heap regions.
- **Memory Restoration**: Restores the saved memory state of the process upon triggering specific conditions.
- **Efficient Process Monitoring**: Utilizes eBPF probes and maps to manage memory checkpoints without significant overhead.
- **BCC Library**: The project uses BCC (BPF Compiler Collection) to interact with eBPF programs.

## How to Build
-------------
1. Run `make` to build the executables.  
2. Run `make clean` to remove the generated executables.

## Content
----------
There are the following files:

- `testcase`:     This file runs the test cases and measures the latency of the memory checkpointing and restoration process.
- `checkpoint`:   Code for handling memory checkpointing and signaling eBPF to start checkpointing or recover process memory.
- `utils`:        Contains implementations of different test cases to simulate various scenarios.
- `answer.py`:    This Python file is used to automate certain operations related to checkpointing and restoration. It interacts with the checkpoint and test case executables, parses input parameters, and generates summary outputs, such as checkpointing and restoration times, memory usage, and logs from eBPF maps.

## Parameters
-------------
The executables accept two parameters:

- `t`: Timeout in seconds (default: 20).
- `n`: Number of elements in the buffer as a power of 2 (default: 1<<10). Use this parameter to configure the program size and buffer capacity.

