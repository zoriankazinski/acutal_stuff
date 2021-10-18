## Assembly

### Resources
- https://github.com/below/HelloSilicon
- https://cs.lmu.edu/~ray/notes/x86assembly/
- https://newbedev.com/how-to-write-hello-world-in-assembler-under-windows
- https://youtu.be/L1ung0wil9Y
- http://asm.sourceforge.net/articles/linasm.html

### How to Run
``` bash
# Create Object File From Code
#   Linux
#    A
gcc -c "filename.s"
#    B
nasm -f elf "filename.s"
#   Mac
as "filename.s" -o "filename.o"
#   Windows
nasm -f win32 "filename.s" -o "filename.o"

# Create Executable From Object File
#   Linux
#    A - with _start:
ld "filename.o" -o "filename"
#    B - with main:
gcc "filename.o" -o "filename"
#   Mac
#    A - with _main:
ld "filename.o" -o "filename"
#    B - with anything else:
ld "filename.o" -p "filename" -e "anything else"
#   Windows
#    Always use _WinMain@16
ld "filename.o" -o "filename"
```

### Basic Code Sample
``` assembly
; LINUX
global _start

section .text
_start:
  mov rax, 1        ; write call (1)
  mov rdi, 1        ; fd 1
  mov rsi, message  ; what to write (address of string)
  mov rdx, 13       ; byte num
  syscall           ; invoke syscall (write)
  mov rax, 60       ; exit call
  xor rdi, rdi      ; exit 0 - xor on the same reg zeros the reg, and rdi is where the exit code is stored.
  syscall           ; invoke syscall (exit)

section .data
message: db "Hello, World", 10



; MAC
.section __TEXT,__text
.global _main
_main:
  movl $0x2000004, %eax         # write call (4)
  movl $1, %edi                 # fd 1
  movq str@GOTPCREL(%rip), %rsi # what to write
  movq $13, $rdx                # byte num
  syscall                       # invoke syscall (write)
  movl %eax, %edi               # ???
  movl $0x2000001, %eax         # exit with return value
  syscall                       # invoke syscall (exit)

.section  __DATA,__data
str:
  .asciz "Hello, World\n"



; WINDOWS - Need to understand how to do without _printf
global _main
extern _printf

section .text
_main:
    push message
    call _printf
    add esp, 4
    ret
message:
  db 'Hello, World', 10, 0
```

### Comments
``` assembly
; this should be the normal comment
# for some reason in mac its hashtag?
```
