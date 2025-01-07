# Transfer Executables Lab

## Objective
Transferred Netcat and SBD executables to an Apache web server and verified file access from a Windows VM. Captured and analyzed network traffic using Wireshark to monitor file transfers between the Kali and Windows machines.

### Skills Learned


### Tools Used
- Kali Linux (Oracle VM)
- Windows VM (Oracle VM)

## Steps
- Get the path for Netcat and SBD
- How to find a path to SBD:

  ┌──(kali㉿kali)-[~]

  └─$ locate sbd.exe

  /usr/share/windows-resources/sbd/sbd.exe

- How to find netcat:
  ┌──(kali㉿kali)-[~]

  └─$ locate nc.exe

  /usr/share/windows-resources/binaries/nc.exe

- Then place netcat and sbd executables in the Apache web server’s root directory:

  Sbd: sudo cp /usr/share/windows-resources/sbd/sbd.exe /var/www/html/

  Netcat: sudo cp /usr/share/windows-resources/binaries/nc.exe /var/www/html/

- Adjusting File Permissions:

  Sbd: sudo chmod 644 /var/www/html/sbd.exe

  Netcat: sudo chmod 644 /var/www/html/nc.exe

- Verify File Access:

Open Web Browser on Kali VM

  Put http://127.0.0.1/sbd.exe then http://127.0.0.1/nc.exe

  If they download successfully; they are ready to be accessed by your
Windows OS

- Access Files from the Windows VM:

Open a web browser on your Windows OS

  Enter: http://<Kali_IP>/sbd.exe

  Enter: http://<Kali_IP>/nc.exe

This ensures that it is working correctly

<img width="494" alt="image" src="https://github.com/user-attachments/assets/a9536627-c3fd-4184-8a44-80f8e2aa88a0" />

- Capture With Wireshark:

Open Wireshark in your Kali VM

Select the interface for the Host-Only network

Apply Capture filter:

  host <Kali-IP> and host <Windows-IP>

<img width="391" alt="image" src="https://github.com/user-attachments/assets/f2eb1208-6117-4a76-b59a-922ccdcb6c63" />


- Access Files from the Windows VM:

  Open a web browser on your Windows OS

  Enter: http://<Kali_IP>/sbd.exe

  Enter: http://<Kali_IP>/nc.exe

  Stop Wireshark capture after they both download, and they should show up on the capture, I put http in the capture filter to narrow down and show the two I am looking for

<img width="468" alt="image" src="https://github.com/user-attachments/assets/3e238e8c-ee78-4c47-a7d2-1820f0ec8190" />

