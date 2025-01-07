# Transfer Executables Lab

## 📝 Objective
Transferred Netcat and SBD executables to an Apache web server and verified file access from a Windows VM. Captured and analyzed network traffic using Wireshark to monitor file transfers between the Kali and Windows machines.


## 🛠️ Skills Learned
- Transferring files via Apache web server
- Adjusting file permissions in Linux
- Capturing and analyzing network traffic with Wireshark
- Using Netcat and SBD for file transfer testing


## 🧰 Tools Used
- Kali Linux (Oracle VM)
- Windows VM (Oracle VM)


## 📋 Steps

### 1️⃣ Get the Path for Netcat and SBD
#### 🔍 How to find the path to SBD:
```bash
┌──(kali㉿kali)-[~]
└─$ locate sbd.exe
/usr/share/windows-resources/sbd/sbd.exe
```


#### 🔍 How to find the path to Netcat:
```bash
┌──(kali㉿kali)-[~]
└─$ locate nc.exe
/usr/share/windows-resources/binaries/nc.exe
```


### 2️⃣ Transfer Executables to Apache Web Server
#### 📂 Place Netcat and SBD executables in the Apache web server's root directory:
```bash
# Copy SBD to the web server directory
sudo cp /usr/share/windows-resources/sbd/sbd.exe /var/www/html/

# Copy Netcat to the web server directory
sudo cp /usr/share/windows-resources/binaries/nc.exe /var/www/html/
```


### 3️⃣ Adjust File Permissions
Set appropriate permissions to ensure files are accessible:
```bash
# Adjust permissions for SBD
sudo chmod 644 /var/www/html/sbd.exe

# Adjust permissions for Netcat
sudo chmod 644 /var/www/html/nc.exe
```


### 4️⃣ Verify File Access on Kali VM
1. Open a web browser on your Kali VM.
2. Enter the following URLs to verify the files can be downloaded:
   - `http://127.0.0.1/sbd.exe`
   - `http://127.0.0.1/nc.exe`

✅ If the files download successfully, they are ready to be accessed from your Windows VM.


<img width="494" alt="image" src="https://github.com/user-attachments/assets/3a304da6-f44e-4996-865c-b994db102f9a" />


### 5️⃣ Capture Traffic with Wireshark
1. Open Wireshark on your Kali VM.
2. Select the interface for the Host-Only network.
3. Apply the following capture filter to focus on traffic between the two machines:
   ```bash
   host <Kali-IP> and host <Windows-IP>

   ```
<img width="391" alt="image" src="https://github.com/user-attachments/assets/8cbb31cb-0a55-4a86-964f-ebe6bea037b6" />

### 6️⃣ Access Files from the Windows VM
1. Open a web browser on your Windows VM.
2. Enter the following URLs, replacing `<Kali_IP>` with your Kali machine's IP address:
   - `http://<Kali_IP>/sbd.exe`
   - `http://<Kali_IP>/nc.exe`


### 7️⃣ Verify Network Traffic in Wireshark
1. Download the sbd.exe and nc.exe files from the Windows VM.
2. Stop the Wireshark capture after both files have been downloaded.
3. Apply a filter in Wireshark to narrow down the capture and focus on HTTP traffic:
   ```bash
   http
   ```


✅ You should see the file transfers captured in Wireshark.

<img width="468" alt="image" src="https://github.com/user-attachments/assets/917e90f7-6054-450f-8ff2-96a5caec5acd" />

### Summary
In this lab, Netcat and SBD executables were successfully transferred to an Apache web server and accessed from a Windows VM. Wireshark was used to capture and analyze the network traffic generated during the file transfers. The exercise demonstrates essential skills in file transfer, web server management, and network traffic analysis in a controlled virtual environment.
