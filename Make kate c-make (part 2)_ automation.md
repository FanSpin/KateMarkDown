Make kate c-make (part 2): automation

c-make is my real interest.  can you show me h"hello world" with the automation?

## CMake Hello World — Full Walkthrough

### 1\. Project Structure

hello/  
├── CMakeLists.txt  
└── src/  
    └── main.c   

### 2\. Source File — src/main.c

**\#include \<stdio.h\>**

**int main(void) {**  
    **printf("Hello, World\!\\n");**  
    **return 0;**  
**}**   

### 3\. Build Description — CMakeLists.txt (project root)

**cmake\_minimum\_required(VERSION 3.16)**  
**project(hello LANGUAGES C)**

**add\_executable(hello src/main.c)**   

That's the entire build system. Three lines:

* cmake\_minimum\_required — CMake refuses to run on older versions  
* project — names the project and tells CMake to find a C compiler (not C++, not Fortran)  
* add\_executable — declares a target called hello built from src/main.c

### 4\. Build Commands (run from the project root)

**\# Configure: reads CMakeLists.txt, finds compiler, generates build system**  
**cmake \-S . \-B build**

**\# Build: compiles \+ links**  
**cmake \--build build**   

That's it. Two commands. Here's what each does:

| Command | What happens | Files produced |
| :---- | :---- | :---- |
| cmake \-S . \-B build | Configure step — parses CMakeLists.txt, locates gcc, generates a Makefile (or Ninja file) | build/Makefile, build/CMakeCache.txt, build/CMakeFiles/ |
| cmake \--build build | Build step — runs the generated Makefile, which invokes gcc for each phase | build/CMakeFiles/hello.dir/src/main.c.o (object file), build/hello (executable) |

### 5\. Run It

**./build/hello**   

### 6\. Rebuild After Editing

**\# Just re-run the build — CMake detects the changed .c file and recompiles only what's needed**  
**cmake \--build build**   

You do not need to re-run the configure step unless you change CMakeLists.txt itself.

### *What CMake Actually Generated (under the hood)*

If you peek into build/CMakeFiles/hello.dir/src/main.c.o — that's the object file from the previous answer. The generated Makefile is essentially:

**gcc \-c src/main.c \-o CMakeFiles/hello.dir/src/main.c.o**  
**gcc CMakeFiles/hello.dir/src/main.c.o \-o hello**   

CMake just automates and tracks those calls so you don't have to.

### Optional: Use Ninja (faster, parallel by default)

**cmake \-S . \-B build \-G Ninja**  
**cmake \--build build**   

Install Ninja with your package manager (sudo apt install ninja-build or sudo dnf install ninja-build).

### In Kate Specifically

In Kate's Build & Run plugin, set:

* Build command: cmake \-S %p \-B %p/build && cmake \--build %p/build  
* Run command: %p/build/hello

(%p \= current file's directory). One click configures \+ builds \+ runs.

