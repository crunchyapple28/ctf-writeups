## PW Crack 1 - 

## Challenge 
<img width="344" height="126" alt="Screenshot 2026-08-08 at 23 29 30" src="https://github.com/user-attachments/assets/dedcb4a5-db35-48cf-9677-d6b2ecf84f4f" />

## initial thoughts

the name of the challenge itself indicates that we'll be doing password cracking (recovering the password, either through guessing, brute force, dictionaries etc)

first i open a temporary directory with cd /tmp which allows me to download the given files in temporary storage
then, in the same directory, i downloaded both the password checker and the encrypted flag
then, upon running level1.py using python3 we get a prompt "Please enter correct password for flag: "

```bash
python3 level1.py
Please enter correct password for flag:
```

my best guess was that the password was stored somewhere in the script in some sort of *if* statement, so i open the level1.py using nano to read the code.
reading it we see the password, and after the password is typed in, the script passes the encrypted contents and the user-supplied password to str_xor(), which XOR-decrypts the flag using the password as the key.

<img width="399" height="62" alt="Screenshot 2026-08-08 at 23 47 09" src="https://github.com/user-attachments/assets/ad5ab6c9-95c9-4c63-8680-7e711b66eef8" />


## PW Crack 2-

the next challenge in the series follows the same principle; 
we get a password checker and an encrypted flag file (level2.flag.txt.enc), when inspecting the password checker using nano, we see the following line 

``` bash
if( user_pw == chr(0x34) + chr(0x65) + chr(0x63) + chr(0x39) ):
        print("Welcome back... your flag, user:")
```

converting the hexadecimal values 0x34, 0x65, 0x63 and 0x39 into their corresponding ascii characters, we get 4ec9.


running level2.py, we get the same prompt as last time (Please enter correct password for flag), and when we paste in 4ec9 it decrypts level2.flag.txt.enc and we get the flag!
