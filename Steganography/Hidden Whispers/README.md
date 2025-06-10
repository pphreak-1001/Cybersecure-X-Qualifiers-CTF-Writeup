### Writeup:

So the provided file was a corrupt PNG file whose PNG and IHDR chunk was missing. 

I used pngcheck and hexeditor to fix the image and got the flag:

```
┌──(root💀lsd-KingdomIntact)-[~]
└─# file data
data: data

┌──(root💀lsd-KingdomIntact)-[~]
└─# strings data
W%KW
XXXX
GIDATx
ZW4! L
!gLsP
Y{uRk
qu      8
}ru5
>;?Hy
IEND

```

The IEND chunk made me realise that it should be an image file.

Fixing the image:

Incorrect:
![image](https://github.com/user-attachments/assets/e14655e8-90bb-424a-a84a-ebb9d0652396)

Corrected:
![image](https://github.com/user-attachments/assets/28079f80-fddc-4760-85cb-154e71681eb1)

Flag:

![image](https://github.com/user-attachments/assets/d87db16a-5d69-4829-aeb6-bec0b6048d95)
