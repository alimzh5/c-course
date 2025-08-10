### CPU and Task Scheduling
* The operating system runs on hardware and manages scheduling so that multiple programs can share the CPU.

* On a single-core CPU, parallel execution is an illusion created by rapidly switching tasks (time slicing).

* If too many tasks are running, the system slows down, and high CPU usage can reach 100%.

* CPU-intensive tasks (e.g., infinite loops) keep the CPU busy and block other work.

* A single program can use only one core unless it is multi-threaded or parallelized.

* Some code is dependent (sequential) and cannot be split across cores.

### CPU Frequency
* CPUs have a clock frequency (e.g., 2.4 GHz) meaning 2.4 billion cycles per second.

* Frequency can be fixed or variable (e.g., 2.4–2.9 GHz).

* Each instruction may require multiple cycles to complete.

* Higher frequency → faster execution, but more power usage and heat.

* CPUs can boost frequency temporarily under high load (dynamic frequency scaling).
****

**/proc Folder**
* A virtual filesystem where the kernel shares reports, status, and information with user space.

**Syscalls**
* Functions that allow user programs to request services from the kernel.

* Involve context switching, so they are slower than pure CPU operations.

**CPU-Intensive vs I/O-Intensive**
* CPU-Intensive: Tasks that require heavy computation (e.g., math loops).

* I/O-Intensive: Tasks that mainly wait for input/output (disk, network, sleep, etc.) and use little CPU.

* Mixed workloads may still be called CPU-intensive if computation dominates.

**OS Scheduling**
* In time-sharing systems, too many tasks can cause delays and missed deadlines.

**RTOS (Real-Time Operating System)**
* Guarantees that a task will run at a specific time, unlike general time-sharing OS where delays are possible.

****

**FreeRTOS** – A lightweight, open-source real-time operating system widely used in embedded and IoT devices.

**Zephyr** – A scalable, open-source real-time operating system designed for embedded devices, supporting multiple architectures.
****
