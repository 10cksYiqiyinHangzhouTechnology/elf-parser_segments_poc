# elf-parser_segments_poc

## Vulnerability type

Dos(Denial of service vulnerability). Attackers cause denial of service through carefully constructed malicious files.

## Project address

[elf-parser address](https://github.com/finixbit/elf-parser)

## Poc address

[afl_segments](https://github.com/10cksYiqiyinHangzhouTechnology/elf-parser_segments_poc/blob/main/afl_segments)

[asan_segments](https://github.com/10cksYiqiyinHangzhouTechnology/elf-parser_segments_poc/blob/main/asan_segments)

[poc file](https://github.com/10cksYiqiyinHangzhouTechnology/elf-parser_segments_poc/blob/main/id3)

## ASAN reports

```bash
ubuntu@ubuntu:~/Desktop/elf-parser/examples/elf-parser/examples$ ./asan_segments id03 
=================================================================
==1022431==ERROR: AddressSanitizer: unknown-crash on address 0x7ffff7fb1000 at pc 0x555555562f82 bp 0x7fffffffdac0 sp 0x7fffffffdab0
READ of size 8 at 0x7ffff7fb1000 thread T0
    #0 0x555555562f81 in elf_parser::Elf_parser::get_segments() ../elf_parser.cpp:66
    #1 0x555555559288 in main /home/ubuntu/Desktop/elf-parser/examples/elf-parser/examples/segments.cc:17
    #2 0x7ffff705f082 in __libc_start_main ../csu/libc-start.c:308
    #3 0x5555555586ad in _start (/home/ubuntu/Desktop/elf-parser/examples/elf-parser/examples/asan_segments+0x46ad)

Address 0x7ffff7fb1000 is a wild pointer.
SUMMARY: AddressSanitizer: unknown-crash ../elf_parser.cpp:66 in elf_parser::Elf_parser::get_segments()
Shadow bytes around the buggy address:
  0x10007efee1b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10007efee1c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10007efee1d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10007efee1e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10007efee1f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x10007efee200:[fe]fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe
  0x10007efee210: fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe
  0x10007efee220: fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe
  0x10007efee230: fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe
  0x10007efee240: fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe
  0x10007efee250: fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe fe
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:       fa
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
  Shadow gap:              cc
==1022431==ABORTING
```
you can see there has a crash when open this poc file.

```
Starting program: /home/ubuntu/Desktop/elf-parser/examples/elf-parser/examples/segments id03

Program received signal SIGSEGV, Segmentation fault.
[----------------------------------registers-----------------------------------]
RAX: 0x87 
RBX: 0x7fffffffddc0 --> 0x4e57004c4c554e ('NULL')
RCX: 0x4160a0 --> 0x100000100 
RDX: 0x25 ('%')
RSI: 0x7fffffffdd98 --> 0x4e57004c4c5500 ('')
RDI: 0x7fffffffdd98 --> 0x4e57004c4c5500 ('')
RBP: 0x7fffffffdde0 --> 0x4500 ('')
RSP: 0x7fffffffdd80 --> 0x1 
RIP: 0x404fa7 (<elf_parser::Elf_parser::get_segments()+615>:	)
R8 : 0x415218 --> 0x4160a0 --> 0x100000100 
R9 : 0xb0 
R10: 0x638000 --> 0x638010 --> 0x0 
R11: 0xfffffffffffff000 
R12: 0x415218 --> 0x4160a0 --> 0x100000100 
R13: 0xf1e8 
R14: 0x7fffffffde98 --> 0x636ed0 --> 0x636ee0 --> 0x52444850 ('PHDR')
R15: 0x7ffff7ffefe8 --> 0x0
EFLAGS: 0x10202 (carry parity adjust zero sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
   0x404f98 <elf_parser::Elf_parser::get_segments()+600>:	
    lea    rbx,[rsp+0x40]
   0x404f9d <elf_parser::Elf_parser::get_segments()+605>:	
    movups xmm0,XMMWORD PTR [r15+0x8]
   0x404fa2 <elf_parser::Elf_parser::get_segments()+610>:	
    movups XMMWORD PTR [rsp+0x70],xmm0
=> 0x404fa7 <elf_parser::Elf_parser::get_segments()+615>:	
    movups xmm0,XMMWORD PTR [r15+0x18]
   0x404fac <elf_parser::Elf_parser::get_segments()+620>:	
    movups XMMWORD PTR [rsp+0x80],xmm0
   0x404fb4 <elf_parser::Elf_parser::get_segments()+628>:	
    mov    rax,QWORD PTR [r15+0x28]
   0x404fb8 <elf_parser::Elf_parser::get_segments()+632>:	
    mov    QWORD PTR [rsp+0x90],rax
   0x404fc0 <elf_parser::Elf_parser::get_segments()+640>:	
    lea    rdx,[r15+0x4]
[------------------------------------stack-------------------------------------]
0000| 0x7fffffffdd80 --> 0x1 
0008| 0x7fffffffdd88 --> 0x7fffffffdd98 --> 0x4e57004c4c5500 ('')
0016| 0x7fffffffdd90 --> 0x0 
0024| 0x7fffffffdd98 --> 0x4e57004c4c5500 ('')
0032| 0x7fffffffdda0 --> 0x7fffffffde70 --> 0x7fffffffde80 --> 0x7f0033306469 
0040| 0x7fffffffdda8 --> 0x7fffffffde98 --> 0x636ed0 --> 0x636ee0 --> 0x52444850 ('PHDR')
0048| 0x7fffffffddb0 --> 0x7fffffffddc0 --> 0x4e57004c4c554e ('NULL')
0056| 0x7fffffffddb8 --> 0x4 
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
Stopped reason: SIGSEGV
elf_parser::Elf_parser::get_segments (this=<optimized out>)
    at ../elf_parser.cpp:66
66	        segment.segment_physaddr = phdr[i].p_paddr;
```
