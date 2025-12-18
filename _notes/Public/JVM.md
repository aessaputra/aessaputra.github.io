---
title: JVM - Mesin Virtual yang Menggerakkan Java
aliases:
  - JVM
  - Java Virtual Machine
categories:
  - "[[Posts]]"
tags:
  - jvm
  - runtime
  - virtual-machine
  - bytecode
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/jvm
created: 2025-12-16
published: 2025-12-16
date: 2025-12-16
topics: []
status: "[[Published]]"
feed: show
---

## Pengantar: Jembatan Antara Kode dan Hardware

Java Virtual Machine (JVM) adalah mesin virtual yang menjalankan [[Java]] bytecode, bertindak sebagai layer abstraksi antara aplikasi Java dan operating system. Seperti penerjemah universal yang memahami berbagai dialek, JVM memungkinkan kode Java yang sama berjalan di Windows, Linux, macOS, dan platform lainnya.

JVM bukan hanya runtime environment, tetapi ekosistem kompleks yang mencakup memory management, garbage collection, just-in-time compilation, dan optimizations yang canggih.

## Arsitektur JVM

### Class Loader Subsystem
Bertanggung jawab memuat class files ke memory dan melakukan verification, preparation, dan resolution.

### Runtime Data Areas
- **Method Area**: Menyimpan class-level data
- **Heap**: Memory untuk object instances
- **Stack**: Method call frames untuk setiap thread
- **PC Register**: Program counter untuk tracking execution
- **Native Method Stack**: Untuk native method calls

### Execution Engine
- **Interpreter**: Menjalankan bytecode line by line
- **JIT Compiler**: Mengkompilasi hot code menjadi native machine code
- **Garbage Collector**: Mengelola memory lifecycle

## Implementasi JVM

### HotSpot JVM
Implementasi reference dari [[OpenJDK]], menggunakan adaptive optimization dan advanced garbage collection algorithms.

### Alternative Implementations
- **OpenJ9**: IBM's JVM dengan focus pada memory efficiency
- **GraalVM**: Polyglot virtual machine dengan native image capabilities
- **Azul Zing**: Commercial JVM dengan low-latency garbage collection

## Performance Optimizations

### Just-In-Time Compilation
JVM menganalisis runtime behavior dan mengoptimalkan frequently-executed code paths menjadi native machine code.

### Garbage Collection Strategies
- **Serial GC**: Single-threaded untuk small applications
- **Parallel GC**: Multi-threaded untuk throughput
- **G1GC**: Low-latency untuk large heaps
- **ZGC/Shenandoah**: Ultra-low latency collectors

### Memory Management
Automatic memory management menghilangkan manual memory allocation/deallocation, mengurangi memory leaks dan segmentation faults.

## JVM Languages

JVM tidak terbatas pada Java, tetapi mendukung berbagai bahasa:
- **Kotlin**: Modern language untuk Android dan server development
- **Scala**: Functional programming dengan type safety
- **Groovy**: Dynamic scripting language
- **Clojure**: Lisp dialect untuk functional programming

## Monitoring dan Debugging

JVM menyediakan rich tooling ecosystem:
- **JVisualVM**: Visual profiling dan monitoring
- **JProfiler**: Commercial profiling tool
- **Flight Recorder**: Low-overhead profiling
- **JVMTI**: Tool interface untuk custom monitoring tools

JVM terus berkembang dengan fitur-fitur modern seperti Project Loom (virtual threads), Project Panama (foreign function interface), dan Project Valhalla (value types), memastikan Java ecosystem tetap competitive di era cloud-native computing.