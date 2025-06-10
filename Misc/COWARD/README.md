### Solution

We have a binary given

Its upx packed so we need to unpack the binary

```
upx -d binaryname
```

I decompiled the binary and did some analysis:

Key Observations:
```
Encrypted Strings: There are several strings that are XOR-encrypted in the binary:

data_407100 (XOR key 0x42)

data_4070e0 (XOR key 0x42)

data_4070c0 (XOR key 0x42)

data_407140 (XOR key 0x17) - This appears to be the flag

Flag Decryption: In function sub_401e40() (which shows "Decrypting hidden message"), there's a decryption routine for data_407140 using XOR key 0x17.

Main Flow: The program:

Checks for root privileges (asks for sudo if not root)

Sets up signal handlers

Shows some "hacking" animations

Decrypts and displays the flag at the end
```
Finding the Flag:
```
The flag is stored in data_407140 and is XOR-encrypted with 0x17. We can extract this data and decrypt it.
```

I solved it using gdb

![image](https://github.com/user-attachments/assets/3c6d14a2-bc14-42eb-8f51-d75fb6c73d86)

solve:
```
encrypted_flag = [
    0x71, 0x7b, 0x76, 0x70, 0x6c, 0x7f, 0x23, 0x74,
    0x7c, 0x24, 0x65, 0x48, 0x7a, 0x27, 0x73, 0x24,
    0x48, 0x23, 0x74, 0x63, 0x26, 0x61, 0x23, 0x63,
    0x24, 0x73, 0x48, 0x22, 0x62, 0x74, 0x74, 0x24,
    0x22, 0x22, 0x71, 0x62, 0x7b, 0x7b, 0x6e, 0x36
]

flag = ''.join([chr(b ^ 0x17) for b in encrypted_flag])
print(flag)
```

Flag: flag{h4ck3r_m0d3_4ct1v4t3d_5ucc355fully!}

