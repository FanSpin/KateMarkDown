# BraveAnswers –compile.asm
## Q/A from our "Brave Answers (Ai chat box)"

*“list deceives like NASM  assembly and various*  
 *files like objects (.o) involved in compiling "hello world"*   
 *in assembly”*  
The main deliverables in a NASM "hello world" build are  
 the source, the object file, and the final executable,   
with an optional listing. Here's the pipeline and each file:

| File | Extension | What it is | Produced by |
| :---- | :---- | :---- | :---- |
| Source | .asm | Hand written assembly (hello.asm) | you |
| Object | .o (Linux/ELF) | Relocatable machine code, not yet linked; can't be run directly | nasm (assembler) |
| Listing | .lst | Optional human \-readable dump of the assembled output | nasm \-l |
| Executable | hello, a.out, or hello.exe | Final linked, runnable binary | ld (or gcc) |

Typical Linux (ELF) flow:  
**nasm \-f elf32 hello.asm**            \# \-\> hello.o  
**ld \-m elf\_i386 hello.o \-o hello**    \# \-\> hello (run with ./hello)   

Key points:  
The \-f flag tells nasm the object format:   
elf/elf64 (Linux), win32/win64 (Windows), macho64 (macOS).

The .o file is an ELF relocatable (e.g. "ELF 32-bit LSB relocatable,   
Intel 80386") — it contains the machine code plus extra sections   
the linker needs, but it cannot be executed until linked.

If you only use direct syscalls (write, exit), you link straight with ld.  
 If you call C functions like printf, you link with gcc so the  
 C runtime is pulled in.

The entry point is \_start (standalone) or   
main (when using gcc's C runtime).

So the core deliverables are: .asm → .o/.obj → executable (plus an optional .lst).

