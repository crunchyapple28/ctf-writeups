Hi! 🍏
I'm solving the Trivial Flag Transfer Protocol CTF, which is the last CTF in the digital forensics learning path I'm doing! These have been extremely fun and rewarding to do and this one is just an example of how much you can learn from them.

So, first we download the [tftp.pcapng](https://challenge-files.picoctf.net/c_wily_courier/9f32bef3f1ad1e5a7c5992f3c1e86619ff557537080e163e5a6d9f01070192a9/tftp.pcapng) file, which is just a network capture. You can check this using **file tftp.pcapng**, then jump straight into WireShark.

Wireshark is a free, open-source network protocol analyzer that captures and inspects data traveling across a computer network in real time. It takes raw binary data moving through a network and translates it into a human-readable format.
This was the biggest packet sample I've worked with thus far, despite this one not being considered large either. Most of the network traffic is TFTP, which up until this point i really didn't know much about, but a quick google will tell us that - 

"**Trivial File Transfer Protocol (TFTP)** is a simple, lockstep file transfer protocol that uses UDP port 69. It's designed to be simple and easy to implement, lacking the authentication and features of FTP. TFTP is commonly used for booting diskless workstations, uploading configurations to network devices, and firmware updates. Due to its lack of authentication, it can be a significant security risk when misconfigured." - https://hackviser.com/tactics/pentesting/services/tftp
<img width="567" height="427" alt="image" src="https://github.com/user-attachments/assets/8473adcc-d877-41e0-a6f5-c524957b2674" />

This is the flow of TFTP, a typical client-server architecture.
I applied a filter on the capture frame to see what was sent and received using  **tftp.type**
We can see the files were sent in this order “instructions.txt”, “plan”, “picture1.bmp”, “picture2.bmp”, “picture3.bmp”. Then I tried exporting all of them to see what they contain by clicking File -> Export Object -> …TFTP . For some reason instructions.txt wouldn't export for me / it wasn't reconstructing properly , so I 
spent quite a significant amount of time trying to retrieve this file, but to no avail.  
<img width="1429" height="545" alt="image" src="https://github.com/user-attachments/assets/c9825d5a-183e-40fe-abc0-22693a4c6c76" />

Essentially, what I found is that there was a write request for instructions.txt, but no data blocks, so there's nothing I can read the actual data from.
I applied the filter **tftp.opcode == 3** leaving us with data packets but nothing relating to instructions.txt. This turned out to be an abnormality, and I later found that it contained a clue:

<img width="678" height="106" alt="Screenshot 2026-09-10 at 20 07 18" src="https://github.com/user-attachments/assets/f2217b08-8f79-4fe6-a37b-2d6246026381" />

This is a simple ROT13 encryption, and you can solve it by using 

``echo 'GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA' | tr 'A-Za-z' 'N-ZA-Mn-za-m' `` 

and what you'll get is this message:

<img width="678" height="104" alt="Screenshot 2026-09-10 at 20 09 34" src="https://github.com/user-attachments/assets/41b829b3-023b-408a-a372-aafbcfb0b7e6" />

"TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER. FIGURE OUT A WAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN"

You can also just use a ROT13 decoder, but despite not working with this clue, given the images and the general pattern of CTFs in digital forensics to hide flags in these files, it was enough of an indicator that that's where it'll be.

<img width="1395" height="751" alt="image" src="https://github.com/user-attachments/assets/f2cdf45b-a407-4df2-8581-54a8b36f727b" />

Here we can find the data package relating to plan! The payload of the tftp data packet (the right side of the hex dump) looks like another ROT13 encryption, and plugging it into a decoder will give us this

<img width="879" height="701" alt="Screenshot 2026-09-10 at 19 46 02" src="https://github.com/user-attachments/assets/0ee55c6a-e163-48ea-b622-bff59531238d" />

Now at this point my first instinct was to use zsteg on the images and check them out, but that resulted in me trying to fix homebrew for 4 (four) whole hours, so after wasting the whole day and finding nothing with zsteg, steghide was the next checkpoint!

In hindsight this is quite obvious and perhaps a more natural move than zsteg, especially considering the message we're given. 

Using steghide on images will tell you if it contains embedded data, but steghide typically requires a password, and if you read the message we found by decrypting the rot13, it says 

``**I USED THE PROGRAM AND HID IT WITH DUE DILIGENCE**. CHECKOUT THE PHOTOS``

So this is them literally telling us they used steghide to embed a message / file into the photos with due diligence ending up being our password. The first 2 images gave nothing but when using steghide on the third one it actually extracted a flag.txt file! And there's our flag!


<img width="661" height="382" alt="Screenshot 2026-09-10 at 19 52 01" src="https://github.com/user-attachments/assets/7a26c16a-394e-46be-9dda-7b5d19fefb6c" />




