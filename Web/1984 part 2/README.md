### Writeup

It is a continuation chall or 1984 part 1.

So in the chall, after we log in, the ultimate goal was to cause a system crash.

When you type in SYS DESTROY after loggin in, it will say SECURITY MODULE not loaded

Load the security module with : LOAD SECURITY.SYS

Now do SYS DESTROY and it will say: Invalid memory override

So now we need to override the memory but we need the mem address,

The memmap.doc gave us the memory address we need to override along with the hint required to guess the values needed for the mem address:

![image](https://github.com/user-attachments/assets/54af639c-b6a5-4b32-b5d1-9b6735d183a9)
 
So as per the memmap.doc:

We need to satisfy the condition:

This line from MEMMAP.DOC is the absolute critical piece of information. It told us that to trigger the security override (which was tied to the self-destruct), a specific mathematical condition had to be met: the Exclusive OR (XOR) sum of all 8 bytes in the memory range from 49152 to 49159 had to equal 0x42 (which is 66 in decimal).


Sent this for calculation to calculate the Poke address value for memory override and got rhis:

Values to XOR:

25
51
187
162
113
0
0
0

Sum = 66 0x42

So after all the above steps use these commands:

POKE ADDRESS VALUE
e.g;
POKE 45192 25 
.... so on upto address 45199


Finally you will get a system crash.

I sent the writeup to the admin and got the flag:
![image](https://github.com/user-attachments/assets/9aa9dd48-9951-45af-8256-4c1b0c3a1fbd)

FLAG: 
```
FLAG{C64_BBS_PURGED_SUCCESSFULLY} 
```
