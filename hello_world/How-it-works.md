# How It Works — Hello World Study Guide

This study guide covers the concepts and topics in the Hello World project. It walks through the C compilation pipeline (preprocessing, compilation, assembly, linking) and basic output with `puts()` and `printf()`. Use this for review and study.

---

## Table of Contents

1. [0-preprocessor — The Preprocessing Stage](#0-preprocessor----the-preprocessing-stage)
2. [1-compiler — The Compilation Stage](#1-compiler----the-compilation-stage)
3. [2-assembler — The Assembly Stage](#2-assembler----the-assembly-stage)
4. [3-name — The Linking Stage](#3-name----the-linking-stage)
5. [4-puts.c — Output with `puts()`](#4-putsc----output-with-puts)
6. [5-printf.c — Output with `printf()`](#5-printfc----output-with-printf)
7. [6-size.c — The `sizeof` Operator](#6-sizec----the-sizeof-operator)

---

## 0-preprocessor — The Preprocessing Stage

### What It Does

The script runs: `gcc -E $CFILE -o c`

- **`-E`** — Stop after preprocessing; do not compile, assemble, or link.
- **`$CFILE`** — Environment variable pointing to the C source file.
- **`-o c`** — Write preprocessor output to a file named `c`.

### Concepts

- **Preprocessing** — First stage of turning C source into an executable. Runs before compilation.
- **Preprocessor directives** — `#include`, `#define`, `#ifdef`, etc. are handled here.
- **`#include`** — Replaced by the contents of the specified header file.
- **`#define`** — Macros are expanded; constants are replaced.
- **Comments** — Removed during preprocessing.
- **Result** — “Pure” C code with no macros, includes, or comments left.

### Key Takeaway

Preprocessing turns your `.c` file into an expanded C file that is ready for the compiler.

---

## 1-compiler — The Compilation Stage

### What It Does

The script runs: `gcc -c $CFILE`

- **`-c`** — Compile and assemble, but do not link. Produce an object file (`.o`).
- **`$CFILE`** — C source file to compile.

### Concepts

- **Compilation** — Translates C (or preprocessed C) into assembly language.
- **Assembly** — Turned into machine code and written to an object file.
- **Object file (`.o`)** — Machine code plus symbols. Not yet a runnable program.
- **Why stop before linking?** — Allows separate compilation of multiple files, then linking later.

### Key Takeaway

The compiler turns C into object code. An object file is an intermediate step before linking.

---

## 2-assembler — The Assembly Stage

### What It Does

The script runs: `gcc -S $CFILE`

- **`-S`** — Compile to assembly and stop. Do not assemble or link.
- **Output** — Assembly file (`.s`) with human-readable assembly language.

### Concepts

- **Assembly Code** — Low-level, one step above machine code. Uses mnemonics like `mov`, `push`, `call`.
- **Architecture-Specific** — Assembly depends on the CPU (e.g. x86, ARM).
- **Assembly vs Machine Code** — Assembly is readable; machine code is binary.
- **Compilation Pipeline** — Preprocess → Compile (to assembly) → Assemble (to object) → Link (to executable).

### Key Takeaway

You can inspect the assembly output to see how C constructs map to low-level instructions.

---

## 3-name — The Linking Stage

### What It Does

The script runs: `gcc $CFILE -o cisfun`

- **No `-E`, `-c`, or `-S`** — Full compilation: preprocess, compile, assemble, and link.
- **`-o cisfun`** — Name the final executable `cisfun`.

### Concepts

- **Linking** — Combines object files and libraries into a single executable.
- **Static vs Dynamic Linking** — Static: libraries copied into the binary; dynamic: libraries loaded at runtime.
- **Standard Library** — Functions like `printf`, `puts` come from libraries (e.g. `libc`) that the linker adds.
- **Executable** — Final binary that the OS can run.

### Key Takeaway

The linker produces the final executable by combining your object code with libraries.

---

## 4-puts.c — Output with `puts()`

### What It Does

```c
puts("\"Programming is like building a multilingual puzzle");
```

Prints a string followed by a newline.

### Concepts

- **`puts()`** — Function in `<stdio.h>` that prints a string and adds a newline.
- **Escape Sequences** — `\"` prints a literal double quote.
- **String Literals** — Text in double quotes, e.g. `"hello"`.
- **`<stdio.h>`** — Standard I/O header for input/output functions.
- **`main(void)`** — No parameters; `void` makes that explicit.
- **`return (0)`** — Return success to the OS; 0 is conventional for success.

### Key Takeaway

`puts()` is an easy way to print a string with a newline. No formatting needed.

---

## 5-printf.c — Output with `printf()`

### What It Does

```c
printf("with proper grammar, but the outcome is a piece of art,\n");
```

Prints a string with an explicit newline.

### Concepts

- **`printf()`** — Formatted output and main printing function in C.
- **Format String** — First argument that can contain format specifiers like `%d`, `%s`, `%f`.
- **`\n`** — Newline; `printf` does not add one automatically.
- **`puts()` vs `printf()`** — `puts` adds a newline; `printf` does not unless you specify `\n`.
- **Variadic Function** — `printf` can take many arguments after the format string.

### Key Takeaway

`printf()` is used for formatted output. If you want a newline, add `\n` yourself.

---

## 6-size.c — The `sizeof` Operator

### What It Does

Prints the size in bytes of:
- `char`
- `int`
- `long int`
- `long long int`
- `float`

### Concepts

- **`sizeof`** — Operator that returns the size in bytes of a type or expression.
- **Result Type** — `size_t` (unsigned). Often cast to `unsigned long` for `%lu`.
- **`%lu`** — Format specifier for `unsigned long`.
- **Data Type Sizes** — Depend on the platform; not fixed by the C standard.
- **Typical Sizes (64-bit)** — `char`: 1, `int`: 4, `long`: 8, `long long`: 8, `float`: 4.

### Key Takeaway

`sizeof` lets you inspect memory layout. Sizes vary by architecture and compiler.

---

## Summary: The Compilation Pipeline

```
Source (.c)  →  Preprocess (-E)  →  Compile (-S)  →  Assemble (-c)  →  Link  →  Executable
                 ↓                     ↓                  ↓
           #include, #define      Assembly (.s)      Object (.o)
```

---

## Quick Reference

| File         | GCC Flag | Output / Purpose                      |
|--------------|----------|----------------------------------------|
| 0-preprocessor | `-E`   | Preprocessed source (no macros)        |
| 1-compiler   | `-c`     | Object file `.o`                       |
| 2-assembler  | `-S`    | Assembly file `.s`                     |
| 3-name       | (none)   | Executable (linker)                    |

| Function | Adds newline? | Best for                  |
|----------|---------------|---------------------------|
| `puts()` | Yes           | Simple string output      |
| `printf()` | No (use `\n`) | Formatted output          |

---

*Last updated for review: hello_world project*
