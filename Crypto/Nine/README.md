### Solution

We have a salted hash: $9$0W7u1RS7NbsYoSrUHqmF369A0RSLxdVs4EcyK8LbwFn/C1h

Eventually i first tried to brute the hash using john but it just could not crack and took decades. 

My system was not very efficient to run hashcat as i always ran into : Not enough memory. Lol

So i decided to read about the kind of hash it was and i came across this: It was a Cisco Type 9 hash which uses scrypt algorithm

The fact that hashcat has the capability to crack it but john cant.

I was like: Bruh!!! WTF

I kept exploring around and somehow my luck landed me here: https://www.m00nie.com/juniper-type-9-password-tool/

HEHE

Flag:

![image](https://github.com/user-attachments/assets/ff336f0d-121d-41bb-ba03-f68bd6b6cb2f)
