# Volatility: Challenge CTF

<h2>Description</h2>
In this Digital Forensics task, I used volatility to enumerate different artifacts from a challenge memory dump.    

<h2>Languages and Utilities Used</h2>

- <b>python3</b>
- <b>volatility</b>

<h2>Environments Used </h2>

- <b>Ubuntu</b> 

<br />
<br />
Running windows.info volatility helps enumerate system time and major/minor version of the memory dump. 

![1) ](https://github.com/user-attachments/assets/04668653-6173-402e-9964-19a4f22f58f5)

<br />
<br />
crss.exe is attempting to be csrss.exe core windows process. Suspicious since these processes normally happen at the start. 

![2)](https://github.com/user-attachments/assets/db04ecc3-30ac-4ddc-a872-2b73b792d61e)

<br />
<br />  
Dumping the windows.netstat into a text file and filtering for the malicious crss.exe process shows 3 established connections. 

![3](https://github.com/user-attachments/assets/edadf69a-4d5a-4465-9044-efc679217ae4)

<br />
<br />
Dumping the windows.pstree into a text file and filtering for the malicious crss.exe process shows the full system path. 

![4](https://github.com/user-attachments/assets/a22a2cab-0187-4498-b1f1-109e1421bea0)

<br />
<br />
Dumping the malicious pid of 5676 and 3076 using "python3 vol.py -f ~/Desktop/challenge.vmem -o ~/Desktop/ windows.pslist --pid <5792 or 3076> --dump" then running a sha256sum of each dump pulls their file hashes. 

![5](https://github.com/user-attachments/assets/873929b5-4a56-45b0-ab96-6a5c9772d08e)

<br />
<br />  
Running "python voil.py -f ~/Desktop/challenge.vmem windows.registry.printkey --key "Software\Microsoft\Windows\CurrentVersion\Run" shows the run persistent when looking for the malicious crss.exe. 

![6](https://github.com/user-attachments/assets/740a1dcf-29fd-44c2-979c-ba476e143001)

<br />
<br />
