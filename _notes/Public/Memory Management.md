---
title: Memory Management - Tukang Kebun Digital Go
categories:
  - "[[Posts]]"
tags:
  - golang
  - memory
  - allocation
  - performance
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

## Pengantar: Hierarki Alokasi Cerdas

Memory Management Go adalah **tukang kebun digital yang ahli** dalam mengelola "taman memori" dengan sistem hierarki tiga tingkat yang meminimalkan lock contention dan mengoptimalkan performance.

## Hierarki Alokasi: Sistem Tiga Tingkat

### mcache (Per-P Cache): Taman Pribadi
- **Thread-local cache** untuk setiap logical processor (P)
- Meminimalkan locking untuk alokasi objek kecil
- Direct access tanpa synchronization overhead
- Optimized untuk high-frequency allocations
- Maintains size-segregated free lists untuk different object sizes

### mcentral (Central Lists): Gudang Komunal
- **Central management** untuk `mspan`s berdasarkan size class
- Ketika mcache needs more memory, requests dari mcentral
- Manages lists of `mspan`s dengan sophisticated algorithms
- Balances antara mcache demands dan heap availability
- Implements lock-based synchronization untuk thread safety

### mheap (Page Heap): Manajer Utama
- **Virtual memory manager** untuk entire Go heap
- Berinteraksi dengan OS melalui `sysAlloc` dan `sysFree`
- Allocates dan deallocates pages ke mcentral
- Manages large object allocations langsung
- Coordinates dengan OS untuk memory mapping operations

## Memory Spans: Unit Alokasi Fundamental

### mspan Structure
- **Contiguous pages of memory** sebagai unit alokasi dasar
- Contains metadata tentang object size, allocation status
- Tracks free objects dengan efficient bitmap structures
- Supports different size classes untuk optimal space utilization
- Integrates dengan GC untuk marking dan sweeping

### Object Allocation dalam Spans
- Objects dalam mspan dapat di-zero jika `mspan.needzero` true
- Otherwise, objects diasumsikan already zeroed untuk performance
- Size-segregated allocation reduces fragmentation
- Efficient free list management untuk quick allocation/deallocation

## Integration dengan Runtime Systems

### Scheduler Integration
- **P (Processor) provides access** ke mcache untuk goroutine allocations
- Thread-local caching eliminates contention antar goroutines
- Automatic mcache refilling dari mcentral ketika exhausted
- Coordinates dengan [[Goroutine Scheduler]] untuk optimal performance

### Garbage Collection Coordination
- **mallocgc function** interacts dengan GC system
- Allocates objects sebagai "black" during GC cycle jika write barriers enabled
- GC sweep returns unused memory ke allocator
- Coordinates dengan [[Garbage Collection]] untuk memory reclamation

## Performance Optimizations

### Lock-Free Fast Paths
- mcache operations mostly lock-free untuk common cases
- Size class segregation reduces allocation complexity
- Bulk allocation/deallocation untuk improved throughput
- Cache-friendly data structures untuk better CPU performance

### Memory Layout Optimization
- NUMA-aware allocation strategies pada supported platforms
- Cache line alignment untuk critical data structures
- Minimized memory fragmentation melalui size class design
- Efficient metadata organization untuk reduced overhead

## Memory Allocation Strategies

### Small Object Allocation
- Objects ≤ 32KB allocated melalui mcache/mcentral/mheap hierarchy
- Size classes optimized untuk common allocation patterns
- Fast path allocation dengan minimal overhead
- Automatic size class selection berdasarkan object size

### Large Object Allocation  
- Objects > 32KB allocated directly dari mheap
- Bypasses mcache/mcentral untuk efficiency
- Direct page allocation dari OS ketika necessary
- Special handling untuk very large allocations

### Stack Management
- Goroutine stacks managed sebagai special case
- Dynamic stack growth dan shrinking
- Stack copying untuk compaction
- Integration dengan scheduler untuk stack management

## Memory Statistics dan Monitoring

### Runtime Statistics
- `runtime.ReadMemStats()` provides detailed memory information
- Heap size, allocation rates, GC statistics
- Per-size-class allocation statistics
- System memory usage tracking

### Debugging Tools
- `GODEBUG=gctrace=1` untuk GC dan memory statistics
- Memory profiling melalui `go tool pprof`
- Heap dumps untuk detailed memory analysis
- Integration dengan [[Profiling and Metrics]] system

## Configuration dan Tuning

### Environment Variables
- `GOMEMLIMIT` sets soft memory limit untuk runtime
- `GOGC` influences GC frequency dan memory usage
- `GODEBUG` options untuk memory debugging
- Runtime adjustable parameters untuk specific workloads

### Memory Pressure Handling
- Automatic GC triggering berdasarkan memory pressure
- Cooperative memory management dengan OS
- Graceful degradation under memory constraints
- Emergency GC untuk preventing out-of-memory conditions

---

*Catatan ini mengeksplorasi Memory Management system Go berdasarkan implementasi dalam golang/go runtime.*