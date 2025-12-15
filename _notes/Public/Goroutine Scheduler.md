---
title: Goroutine Scheduler - Konduktor Orkestra Digital
categories:
  - "[[Posts]]"
tags:
  - golang
  - goroutines
  - scheduler
  - concurrency
  - runtime
author:
  - "[[Aes Saputra]]"
url:
created: 2025-12-15
published:
date: 2025-12-15
topics: []
status:
  - "[[Published]]"
feed: show
---

## Pengantar: Maestro Concurrency

Goroutine Scheduler adalah **maestro yang mengatur orkestra concurrency** dalam Go Runtime. Sistem ini mengelola jutaan goroutines dengan overhead minimal, memungkinkan Go mencapai concurrency yang efisien dan scalable.

## Model G-M-P: Arsitektur Tiga Pilar

### G (Goroutine): Musisi dalam Orkestra
- **Lightweight execution unit** yang menyimpan state goroutine
- Berisi stack information dan scheduling metadata
- Dibuat melalui `newproc` function
- Setiap `g` object holds goroutine's complete execution context
- Independently executing function dengan minimal memory footprint

### M (Machine): Panggung Eksekusi  
- **Operating system thread** yang mengeksekusi Go code
- Harus memiliki associated `P` untuk dapat menjalankan Go code
- Ketika M stops executing Go code (system call), returns P ke idle pool
- Represents actual OS-level execution context
- Bridge antara Go runtime dan operating system

### P (Processor): Logical Conductor
- **Logical processor** yang menyediakan resources untuk eksekusi Go code
- Jumlah P ditentukan oleh `GOMAXPROCS` environment variable
- Setiap P memiliki local run queue (`runq`) untuk goroutines
- Provides execution context dan local caching untuk performance
- Acts sebagai resource manager untuk goroutine execution

## Scheduling Algorithm: Work-Stealing Orchestra

### Local Run Queues
- Setiap P maintains local run queue untuk goroutines
- Minimizes contention dengan thread-local scheduling
- LIFO order untuk better cache locality
- Automatic load balancing antar processors

### Global Run Queue
- Fallback queue ketika local queues kosong
- Handles overflow dari local queues
- Ensures fairness dalam goroutine scheduling
- Prevents starvation scenarios

### Work Stealing Mechanism
- Idle P dapat "steal" work dari P lain yang busy
- Maintains load balance across all processors
- Reduces idle time dan maximizes CPU utilization
- Implements sophisticated stealing algorithms untuk fairness

## Scheduler Integration dengan Runtime

### Memory Management Integration
- P provides access ke `mcache` untuk goroutine allocations
- Thread-local caching reduces memory allocation contention
- Coordinates dengan [[Memory Management]] untuk optimal performance
- Manages stack growth dan shrinking untuk goroutines

### Garbage Collection Coordination
- Scheduler assists dalam GC marking melalui `gcAssistAlloc`
- Stop-the-world phases pause semua goroutines
- P objects track `goroutinesCreated` untuk GC statistics
- Coordinates dengan [[Garbage Collection]] untuk memory safety

### System Call Handling
- Goroutines dapat block pada system calls tanpa blocking OS threads
- M releases P ketika entering blocking system calls
- Network poller handles non-blocking I/O operations
- Automatic thread creation/destruction berdasarkan demand

## Performance Characteristics

### Scalability Features
- Supports jutaan goroutines dengan minimal overhead
- O(1) scheduling complexity untuk most operations
- Lock-free algorithms untuk critical paths
- NUMA-aware scheduling untuk modern hardware

### Latency Optimization
- Sub-microsecond context switching
- Cooperative scheduling dengan preemption support
- Priority-based scheduling untuk time-sensitive tasks
- Automatic yield points untuk fairness

## Scheduler Configuration

### GOMAXPROCS Tuning
- Controls jumlah logical processors (P)
- Default: number of CPU cores
- Can be adjusted untuk specific workload characteristics
- Runtime adjustable melalui `runtime.GOMAXPROCS()`

### Scheduler Debugging
- `GODEBUG=schedtrace=X` untuk scheduler tracing
- `GODEBUG=scheddetail=1` untuk detailed scheduling information
- Runtime statistics available melalui `runtime.ReadMemStats()`
- Profiling integration untuk performance analysis

## Advanced Scheduling Features

### Preemptive Scheduling
- Automatic preemption untuk long-running goroutines
- Signal-based preemption pada supported platforms
- Prevents goroutine monopolization of processors
- Maintains responsiveness dalam compute-intensive workloads

### Network Poller Integration
- Efficient handling of network I/O operations
- Event-driven I/O dengan minimal thread usage
- Integration dengan epoll/kqueue/IOCP berdasarkan platform
- Automatic goroutine wake-up pada I/O completion

### Timer Integration
- Efficient timer management dengan minimal overhead
- Heap-based timer organization untuk O(log n) operations
- Integration dengan scheduler untuk timer-based wake-ups
- Supports high-frequency timer operations

---

*Catatan ini mengeksplorasi Goroutine Scheduler berdasarkan implementasi dalam golang/go runtime system.*