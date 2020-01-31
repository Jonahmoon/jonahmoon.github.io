# How to start your first nasm project on MacOs
### update your nasm
```
open your terminal
:brew install nasm
```
### create your first program file helloworld.asm
```asm
SECTION .data
   
msg: db "hello world!", 0x0a
len: equ $-msg
  
SECTION .text
global _main
  
kernel:
     syscall
     ret
 
_main:
     mov rax,0x2000004
     mov rdi,1
     mov rsi,msg
     mov rdx,len
     call kernel
  
     mov rax,0x2000001
     mov rdi,0
     call kernel
```
### Then open terminal in the same directory with asm file, please write the right version of your system such as 10.15
```
:nasm -f macho64 -o helloworld.o helloworld.asm 
:ld -o helloworld -e _main helloworld.o -macosx_version_min 10.15.2 -static 
```
### Now you have a executable file, just run it
```
:./helloworld
```
