# Trainer 
## Trainer 001
- SSH to trainer.pwn.site
- Creds are level0:level0
![Pasted image 20230127120559](https://github.com/user-attachments/assets/0e453ba0-719d-47a0-81cc-9432f8a970b1)
- `cat level1password` == 4202c26842398c1d0772ed9eed195113
- There is a directory in ~ titled **some_directory**.  `cd some_directory`
- `cat level2_password` == 943430e07fd566bc96aa05fca3c96e48

## Trainer 002
- Directories within directories.  The flag is in ``~/dir/another_dir/another_another_dir/some_directory/level3_password`
- 2cadca6148093c403d82396252b8c4db

## Trainer 003
- Challenge hints that you might not see the document with the password at first.  
- `ls -al` shows the file `.level4_password`
- 72f6af6b0005adb15fbc91e1b140115f

## Trainer 004
The password for the next level is in this user's home directory, just like the last levels you might have to dig.

- `ls -alR` shows `.hidden_dir` and then `.level5_password`
- 7b6c2552940f47a27fbd729ae0e2893c

## Trainer 005
For this level the password is in level6's home directory.  Due to a persmissions error, the level5 user can access it.  Think about the directories you have already seen and what file name patterns.
- `cat /home/level6/level6password` == 7cb1963d316b9a302cf6c204d35b7302

## Trainer 006
The password for the next level is in this user's home directory, however this time there are too many directories to manually dig through.  For this level you will need the find command and search for a file that has pass in the title.
- Tried `find . "pass"` at first, then `find . -iname "pass"`.  No hits.
- Realized I'm dumb, I forgot to account that pass is in the title, so can't just use "pass".  `find . -iname "*pass*"` and found that the password for level7 is in `./dir/subdir40/level7_password`
- RG8geW91IGV2ZW4gbGlmdCBicm8g

## Trainer 007
The password for the next level is in the password_directory.  For this level though, all files are exactly the same size.  You should look through each file to find the one that contains the password.
- 99 files, but a bit ain't one
- `cd password_directory/` -> `cat * | grep pass -C 4` == bGV0J3MgZmluZCBzb21ldGhpbmcg

## Trainer 008
For this level the password is in an executable hidden in one of these sub-directories.  When you run the executable it will print out the flag.  To run the executable type: ./executable
- `find . * -type f` finds ./dir24/subdir13/level9_password
- 96ab15e954f1267ea04c35de2d771c2b

## Trainer 009
First a bit of history.  RockYou was a social media site that suffered a security breach in 2009, losing 32 million passwords.  They were storing all the user credentials in plain text in their database.  At the time this was the largest breach of passwords and allowed for academic research and password analysis with real data.  These passwords were eventually organized into a password list that is commonly used for cracking passwords.

For this level we want to find the line number in the rock you wordlist where the password "evilhacker" is found.  That line number is the password for level 10.  The wordlist can be found at /usr/share/wordlists/rockyou.txt (it's in the same place on kali too) Grep uses a 1-based numbering system meaning the first line is 1 and not 0.

- `grep "evilhacker" /usr/share/wordlists/rockyou.txt -n` == 955830:evilhacker

## Trainer 010
# Terror Attack
Using Autopsy 4.20.0, imported the DiskImage.E01 and analyzed it using all available modules.

## 001: Name
One of the first areas that stood out was the E-Meal Messages artifacts.  Data Artifacts > E-Mail Messages > Default > Default shows 1 message.  The sender is rokie(at)pm.me and the receipient is bedulf(at)pm.me.  To confirm, I go to Data Sources > DiskImage.E01_1Host > DiskImage.E01 > Users and see that Bedulf is one of the user accounts on this Windows machine.

What was the codename of the terrorist?
Bedulf

## 002: Country
Looking the email discovered during Question 001, I see in the email header that the originating IP is 119.92.246.150.  Use ipinfo.io to enrich this IP address, which gives me  asn:"AS9299", which is in the Phillipines.

## 003: Group
What's the name of the terrorist group?

Still using the email, I see that at the bottom of the email appears to be a signature.  It has the "name" of the person who sent it, Caption Rokie, and possibly the group they belong to in all caps.

**TERROR007**

## 004: Date
We learned that they planned an attack to take place and informed their operator. Can you uncover the scheduled date of the attack?

```
yc wH wE K^ [B E> LA .> C5 *> #^ 9X 6} Q3 Mq `~ oQ Lu 4L nx *^ mh Vi >O {X [D Y9 TE 1# qQ 7. Hf ,X #4 3$ dm Uc jS ?U ~1 t; R# bO 4j {Q (L pP P^ _u Zr kY << #< {6 &! (y !& bL qU ?6 eN 5f <p }F Fb 9] %+ (+ #D ;y {6 <@ >0 |w xB C{ a? ,a G2 et XF "] U[ |d =) Wv 3} !f P| 0~ =n /! `g ]} F< hP jM G_ aG 2+ PN $c Dp Pr 7U >i [Q )9 Ef pg a| 3r ny VF <= Y7 Qr V4 LH bX vf (^ NU }1 dR
```

01/19/2023 ? 
Flag format: flag{MM/DD/YYYY}

## 005: Password
We discovered an encrypted partition file on the system. We need to decrypt it to go further, but we don't know the password. Can you decrypt the file?

There is a wordlist in C:\Users\Public\Documents

Flag format: flag{password}

## 006: Place

What's the name of the location intended for the attack?

/img_DiskImage.E01/Users/Bedulf/Desktop/sec fol/place.vc

Flag format: flag{location name}

## 007: App
What's the name of the messaging app used by this operator?

Searching further into Bedulf's disk image, start checking under Bedulf/AppData/Roaming for any items of interest.  Find Telegram.exe

Telegram

Flag format: flag{name}

## 008: Weapon
The operator was searching for a very dangerous weapon on the internet. Can you find the name of the weapon?

bomb?  Nova Six Bomb?  Nuclear Bomb?

Flag format: flag{name}

# inbetweenthelines
## inbetween 0x001
GIF of a NyanCat variant.  
Tried aperisolve.com, nothing showed up from the output.
Tried strings with variations of `-n` switch, nothing feasiable.
Opened image with **Image Magick** and one of the frames has the following:
![Pasted image 20230127160540](https://github.com/user-attachments/assets/347586a0-edef-4e18-ba25-f550f92cc822)
flag{sPl1t_53c0nd_v1Ew}

## inbetween 0x002
Same as above, just had to transcribe everything by hand.  It mentions using Optical Character Recognition (OCR), which I briefly tried with CyberChef but had no luck.  Could someone else show me how they could have done that using OCR?

flag{W31C0M3_70_7H3_111_80X_0F_Ur_UN1M461N4813_P41N_4150_15N7_U51N6_4_0Cr_50_C001_11K3_17_15_U53FU1}

## inbetween 0x003
Audio file with two notes.  Binary.  Output is:

0110011001101100011000010110011101111011011011010101010100110101001100010100001101100001011011000101111101100011010010000110000100110001010100100011010101111101

flag{mU51Cal_cHa1R5}
