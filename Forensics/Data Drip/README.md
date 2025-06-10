### Solution

The flag was divided in the packets as base64 encoded subdomain of hackersc2cdo.main in DNS queries.

Solution

```
tshark -r capture.pcapng -Y "dns.qry.name" -T fields -e dns.qry.name | grep "hackersc2cdo.main" | cut -d '.' -f1 | while read l; do echo "$l" | base64 -d 2>/dev/null; echo; done
```

![image](https://github.com/user-attachments/assets/a2f7889f-2c66-4b54-bda5-6587f821aef9)
