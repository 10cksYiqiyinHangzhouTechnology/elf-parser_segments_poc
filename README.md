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
