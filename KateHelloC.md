KateHelloC

list the and explain the steps needed to compile  
 "c language" hello world including various file  
 types (e.g. source code, CMakeList, objects) 

## Source Code (.c)

**\#include \<stdio.h\>**  
**int main() {**  
    **printf("Hello, World\!\\n");**  
    **return 0;**  
**}**   

## The Four Compilation Phases

| Phase | Input | Output | GCC Command |
| :---- | :---- | :---- | :---- |
| Preprocessing | hello.c | hello.i | gcc \-E hello.c \-o hello.i |
| Compilation | hello.i | hello.s | gcc \-S hello.i \-o hello.s |
| Assembly | hello.s | hello.o | gcc \-c hello.s \-o hello.o |
| Linking | hello.o | hello (executable) | gcc hello.o \-o hello |

1. Preprocessing — Expands \#include directives (inlines stdio.h), replaces \#define macros, and strips comments. The output is a plain C file (.i) with all directives resolved.  
2. Compilation — Translates the preprocessed C into assembly language (.s). This is where syntax errors are caught and optimizations are applied.  
3. Assembly — Converts the assembly (.s) into machine code, producing an object file (.o). The object file contains binary instructions but has unresolved references (e.g., printf is not yet linked).  
4. Linking — Combines all object files with required libraries (e.g., libc for printf) to resolve all symbols and produce the final executable (no extension on Linux, .exe on Windows). 

## One-Liner (what most people actually type)

This runs all four phases in sequence, discarding intermediate files.

## CMakeLists.txt (Build Automation)

For larger projects, you describe the build in a CMakeLists.txt file instead of typing raw gcc commands:

**cmake\_minimum\_required(VERSION 3.10)**  
**project(hello C)**  
**add\_executable(hello hello.c)**   

Then build with:

**cmake \-B build**  
**cmake \--build build**   

CMake generates the appropriate compiler/linker commands (and a Makefile or equivalent) under the hood — it orchestrates the same four phases but scales to multi-file projects, libraries, and cross-compilation.

## File Type Summary

| Extension | What it is |
| :---- | :---- |
| .c | C source code |
| .h | Header file (declarations, macros) |
| .i | Preprocessed source |
| .s | Assembly code |
| .o / .obj | Object file (machine code, unlinked) |
| CMakeLists.txt | CMake build description |
| *(none)* / .exe | Final executable |

