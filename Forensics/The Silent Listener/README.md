### Solution

We have a pcap file for ananlysis.

I used wireshark and filtered the packets based on its length

There was a POST request made to /upload with a ZIP file being uploaded. 

![image](https://github.com/user-attachments/assets/2dd25f63-4b39-4ee5-b043-1c203015b5f4)

I used binwalk to extract the zip from the pcap.

The zip was password protected. I used john to crack the pass and got the flag.
