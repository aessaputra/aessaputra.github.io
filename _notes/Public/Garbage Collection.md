---
title: Garbage Collection - Petugas Kebersihan Otomatis Memory
aliases:
  - Garbage Collection
  - GC
  - Memory Cleanup
  - Automatic Memory Management
categories:
  - "[[Posts]]"
tags:
  - garbage-collection
  - memory-management
  - runtime
  - performance
  - programming-languages
author:
  - "[[Aes Saputra]]"
url:
created: 2025-12-16
published: 2025-12-16
date: 2025-12-16
topics: []
status: "[[Published]]"
feed: show
---

## Pengantar: Robot Pembersih Universal dalam Dunia Pemrograman

Garbage Collection adalah **sistem manajemen memori otomatis** yang bertindak seperti petugas kebersihan pintar di berbagai bahasa pemrograman modern. Seperti robot vacuum yang tahu kapan dan di mana harus membersihkan tanpa mengganggu aktivitas penghuni rumah, GC secara otomatis mengidentifikasi dan membersihkan objek-objek yang tidak lagi digunakan dalam program.

Konsep ini hadir di berbagai bahasa seperti [[Java]], [[JVM]] languages, Go, C#, Python, JavaScript, dan banyak lagi, masing-masing dengan implementasi dan karakteristik yang unik sesuai dengan filosofi dan kebutuhan bahasa tersebut.

## Algoritma Fundamental Garbage Collection

### Mark-and-Sweep: Algoritma Klasik

**Mark-and-Sweep** adalah algoritma foundational yang digunakan dalam berbagai implementasi GC:

```mermaid
graph TD
    A[Root Objects<br/>Stack, Globals] --> B[Mark Phase<br/>Traverse & Mark Reachable]
    B --> C[Sweep Phase<br/>Reclaim Unmarked Objects]
    C --> D[Compaction<br/>Optional Defragmentation]
    
    E[White Objects<br/>Unmarked] --> F[Gray Objects<br/>Being Processed]
    F --> G[Black Objects<br/>Marked as Reachable]
    
    style A fill:#e1f5fe
    style B fill:#f3e5f5
    style C fill:#e8f5e8
    style D fill:#fff3e0
```

**Tri-Color Abstraction** (digunakan dalam Go, beberapa JVM GC):
- **White**: Objek belum dikunjungi, kandidat untuk dibersihkan
- **Gray**: Objek sedang diproses, dalam antrian pemeriksaan  
- **Black**: Objek sudah diproses dan confirmed reachable

## Implementasi GC Across Languages

### Java/JVM Ecosystem
**HotSpot JVM** menyediakan berbagai GC algorithms:

| GC Algorithm | Characteristics | Use Case |
|--------------|----------------|----------|
| **Serial GC** | Single-threaded, STW | Small applications |
| **Parallel GC** | Multi-threaded, throughput-focused | Batch processing |
| **G1GC** | Low-latency, region-based | Large heaps, interactive apps |
| **ZGC/Shenandoah** | Ultra-low latency, concurrent | Real-time applications |

### Go Runtime GC
- **Tri-color concurrent collector** dengan minimal STW pauses
- **Write barriers** untuk concurrent marking
- **Pacing algorithm** untuk adaptive triggering

### .NET/C# GC
- **Generational collection** dengan multiple generations
- **Background GC** untuk server applications
- **Workstation vs Server modes** untuk different scenarios

### Python GC
- **Reference counting** sebagai primary mechanism
- **Cycle detection** untuk handling circular references
- **Generational collection** untuk optimization

### JavaScript V8 GC
- **Orinoco collector** dengan incremental marking
- **Scavenger** untuk young generation
- **Mark-Compact** untuk old generation

## Strategi dan Teknik GC Universal

### Generational Hypothesis
**Konsep fundamental** yang digunakan di Java, .NET, Python:
- **Young objects** cenderung mati lebih cepat
- **Old objects** cenderung hidup lebih lama
- **Separate collection strategies** untuk different generations

### Concurrent vs Stop-the-World
```mermaid
graph LR
    A[STW GC] --> B[Application Paused]
    B --> C[Complete Collection]
    C --> D[Resume Application]
    
    E[Concurrent GC] --> F[Parallel Execution]
    F --> G[Minimal Pauses]
    G --> H[Continuous Operation]
    
    style A fill:#ffebee
    style E fill:#e8f5e8
```

### Write Barriers dan Read Barriers
- **Write barriers**: Track pointer modifications during concurrent collection
- **Read barriers**: Ensure consistent view during concurrent phases
- **Implementation varies** across different runtime systems

## Performance Characteristics dan Trade-offs

### Latency vs Throughput Spectrum
| Priority | GC Strategy | Examples | Trade-offs |
|----------|-------------|----------|------------|
| **Low Latency** | Concurrent, Incremental | ZGC, Shenandoah, Go GC | Higher CPU overhead |
| **High Throughput** | Parallel, Batch | Parallel GC, G1GC | Longer pause times |
| **Balanced** | Generational, Adaptive | HotSpot G1, .NET GC | Moderate both |

### Memory Overhead Considerations
- **GC metadata** requires additional memory
- **Write barriers** add runtime overhead
- **Concurrent algorithms** need extra bookkeeping structures

## Language-Specific Tuning dan Configuration

### Java/JVM Tuning
```bash
# G1GC configuration
-XX:+UseG1GC -XX:MaxGCPauseMillis=200 -XX:G1HeapRegionSize=16m

# ZGC for ultra-low latency
-XX:+UseZGC -XX:+UnlockExperimentalVMOptions
```

### Go GC Configuration
```bash
# Environment variables
GOGC=100          # GC frequency (default 100%)
GOMEMLIMIT=4GiB   # Soft memory limit
GODEBUG=gctrace=1 # GC statistics
```

### .NET GC Settings
```xml
<configuration>
  <runtime>
    <gcServer enabled="true"/>
    <gcConcurrent enabled="true"/>
  </runtime>
</configuration>
```

## Advanced GC Concepts

### Weak References dan Finalization
- **Weak references**: References yang tidak mencegah GC
- **Finalizers**: Cleanup code sebelum object destruction
- **Phantom references**: Post-mortem notifications

### Escape Analysis dan Stack Allocation
- **Compiler optimization** untuk avoiding heap allocation
- **Stack allocation** untuk short-lived objects
- **Reduced GC pressure** melalui smart allocation strategies

## Advanced Features

### Write Barriers: Sentinel Guards
- **Hybrid write barriers** track pointer modifications during concurrent marking
- Ensures no reachable objects missed during concurrent phase
- Minimal overhead pada normal operations

### Finalizers dan Weak References
- **Finalizers** untuk cleanup resources sebelum object reclaimed
- Careful ordering untuk avoid resurrection scenarios
- Integration dengan resource management patterns

## Monitoring dan Debugging

### GC Statistics
```go
var stats runtime.MemStats
runtime.ReadMemStats(&stats)
// Access GC timing, frequency, pause times
```

### Profiling Integration
- **GC profiling** melalui go tool pprof
- Heap dumps untuk memory leak detection
- Integration dengan [[Profiling and Metrics]] ecosystem

## Best Practices untuk GC-Friendly Code

### Memory Allocation Patterns
- **Pool objects** untuk reducing allocation pressure
- Avoid excessive small allocations
- Reuse buffers dan data structures when possible

### Pointer Management
- **Minimize pointer chains** untuk faster marking
- Use value types when appropriate
- Careful dengan circular references

---

*Catatan ini mengeksplorasi Garbage Collection system Go berdasarkan implementasi tri-color concurrent collector dalam golang/go runtime.*