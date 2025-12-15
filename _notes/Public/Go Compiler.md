---
title: Go Compiler Architecture - Pabrik Transformasi Kode
categories:
  - "[[Posts]]"
tags:
  - golang
  - compiler
  - ssa
  - optimization
  - code-generation
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

## Pengantar: Pipeline Transformasi Multi-Stage

Go Compiler adalah **pabrik transformasi kode** yang mengubah source code Go menjadi executable machine code melalui pipeline multi-stage yang terdiri dari Frontend, Middle End, dan Backend.

## Frontend: Quality Control Awal

### Parsing dan AST Generation
- Package `cmd/compile/internal/syntax` menangani lexical analysis dan parsing
- Menghasilkan `syntax.File` AST untuk setiap source file
- Proses dimulai dengan `syntax.Parse`

### Type Checking dengan types2
- Package `cmd/compile/internal/types2` (port dari `go/types`) melakukan type checking
- Melakukan type inference, function instantiation untuk generics
- Method resolution, interface satisfaction checks, dan constant evaluation
- Output: typed AST dan IR tree menggunakan `ir.Node` types

## Middle End: SSA Generation dan Optimizations

### SSA Generation: Transformasi ke Single Assignment
- `ssagen.buildssa` mengkonversi `ir.Func` menjadi `ssa.Func`
- Dalam SSA form: setiap variabel assigned tepat sekali
- Control flow explicit via blocks dan edges
- Phi functions digunakan di control flow merge points
- Core types: `ssa.Func`, `ssa.Block`, `ssa.Value`

### Optimization Passes: Tim Efisiensi

#### Prove Pass - Detektif Logika
- File: `ssa/prove.go`
- Maintains `factsTable` untuk melacak relations antar SSA values
- Eliminasi redundant bounds checks dan branches
- Fact propagation untuk optimasi yang lebih agresif

#### Rewrite Rules - Ahli Renovasi Kode  
- Pattern-matching rules untuk simplifikasi SSA operations
- Defined in `_gen/generic.rules` untuk architecture-independent optimizations
- Contoh: `(Add64 (Const64 [c]) (Const64 [d])) → (Const64 [c+d])`
- Code-generated ke functions seperti `rewritegeneric.go`

#### Inlining - Penghilang Perantara
- Function inlining expands function calls langsung ke caller's code
- Mengurangi overhead dan meningkatkan execution speed
- Part of middle end optimizations

## Backend: Code Generation Architecture-Specific

### Architecture Lowering
- Generic SSA operations → architecture-specific operations
- Menggunakan rewrite rules dalam files seperti `_gen/AMD64.rules`, `_gen/ARM64.rules`
- Contoh: `(Add64 ...)` → `(ADDQ ...)` pada AMD64

### Register Allocation
- Assigns SSA values ke machine registers atau stack locations
- Manages register pressure dan adheres to calling conventions
- Critical untuk performance optimization

### Code Generation
- Traverses register-allocated SSA dan emits `obj.Prog` assembly instructions
- Package `obj` menyediakan architecture-independent representation of assembly
- `ssagen.Compile` orchestrates SSA backend, generating `plist`

## Compilation Pipeline Flow

```
Source Code (.go) 
    ↓ syntax.Parse
AST (syntax.File)
    ↓ types2.Check  
Typed AST + IR (ir.Node)
    ↓ ssagen.buildssa
SSA Form (ssa.Func)
    ↓ Optimization Passes
Optimized SSA
    ↓ Architecture Lowering
Architecture-Specific SSA
    ↓ Register Allocation
Register-Allocated SSA
    ↓ Code Generation
Assembly (obj.Prog)
    ↓ Linker
Executable
```

## Debugging dan Development Tools

### GOSSAFUNC Environment Variable
- Useful tool untuk debugging dan visualizing SSA form
- Dapat melihat SSA pada berbagai compilation stages
- Essential untuk compiler development dan optimization analysis

### Compiler Phases Overview
- `gc.Main` function orchestrates entire pipeline
- `ssa.Compile` iterates through optimization passes
- Passes defined dalam `passes` list di `ssa/compile.go`

## Key Implementation Files

- `cmd/compile/README.md`: Comprehensive compiler phases overview
- `cmd/compile/internal/ssa/README.md`: SSA backend specifics  
- `src/cmd/compile/internal/ssa/compile.go`: Pass management
- `_gen/*.rules`: Architecture-specific dan generic rewrite rules

---

*Catatan ini mengeksplorasi arsitektur Go Compiler berdasarkan dokumentasi teknis golang/go repository.*