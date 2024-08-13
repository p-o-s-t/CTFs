## General

### Commitment Issues
After downloading the attached zip file, check the folder with `ls -la` to see that there is a `.git` folder.  Using `git log` tells us that there was a previous commit that had the flag in it.  Use `git show <commit ID/HEAD>` to get the information. -> picoCTF{s@n1t1z3_cf09a485}

### Time Machine
Basically the same as [[picoCTF 2024#Commitment Issues|Commitment Issues]], except you just need to use `git log` to get the flag.  -> picoCTF{t1m3m@ch1n3_8defe16a}

### Blame Game
Same idea as previous, but there's a lot of commit messages this time around.  Find the one that stands out by using `git log | grep "Author:" | uniq` to get the flag -> picoCTF{@sk_th3_1nt3rn_cfca95b2}

### Collab
Had to use a hint here.  There are several branches, which you can see with `git branch -a`.  The different parts of the flag are in each branch, which you can switch between using `git checkout <branch>`.  Then `git show HEAD` and you get the pieces of the flag that becomes -> picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_7ae8dd33}

## Cryptography

### interencdec
The file contains a base64 encoded message, which is another base64 message but in byte format, which has the flag but it's been rotated.  
- YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyMHdNakV5TnpVNGZRPT0nCg==
- `b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrX20wMjEyNzU4fQ=='`
- wpjvJAM{jhlzhy_k3jy9wa3k_m0212758} 
- ROT19
The [cyberchef recipe](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)Drop_bytes(0,2,false)Drop_bytes(48,2,false)From_Base64('A-Za-z0-9%2B/%3D',true,false)ROT13(true,true,false,19)&input=WWlka00wSnhaR3R3UWxSWWRIRmhSM2cyWVVoc1ptRjZUbkZsVkd3eldWUk9jbGd5TUhkTmFrVjVUbnBWTkdaUlBUMG5DZz09), if you don't want to do this by hand in terminal.

## Web Exploitation

### IntroToBurp
Using the provided hint and site, open up BurpSuite to start capturing traffic between you and the target.  Had to use all the hints to find that it wants you to mess with the client request to produce an unusual server response.  Once I got to the 2FA screen, I sent the POST request from Proxy to Repeater and just started messing with the body of the request.  I deleted the variable `otp` from the body of the request and that did the trick -> picoCTF{#0TP_Bypvss_SuCc3$S_3e3ddc76}

## Reverse Engineering

### packer
After downloading the file, I ran strings to see if there is anything I can read without having to do anything else.  There is some text, but nothing of value.  The end of the file lists `UPX`, a packer used for executable files.  This is present on my linux box, so I used `upx -d out` to get the unpacked version.  I try strings again and look for anything that mentions password: `strings out | grep -n -C 4 password`.  The output looks like hex, so I throw it into Cyberchef real quick and get the flag -> picoCTF{U9X_UnP4ck1N6_B1n4Ri3S_e190c3f3}

## Forensics

### Scan Surprise
It's just a qr code that needs to be scanned.  `picoCTF{p33k_@_b00_0194a007}`

### Verify
You're given a couple of files for this one, one of which is a checksum using SHA256.  You can ignore the shell script, which really just has some clues on what to do next if you're stuck.  I use `sha256sum files/* | grep <checksum>` to identify which file is the right one.  Afterwards, I spin up the instance from PicoCTF, use the `decrypt.sh files/<file>` on the file I IDed earlier and get the flag.  ->picoCTF{trust_but_verify_e018b574}

### CanYouSee
After you unzip the challenge file, you get an image file.  I decided to use `exiftool` on it first and see that one of the lines of metadata is base64 encoded, which gives me the flag of picoCTF{ME74D47A_HIDD3N_b32040b8}

### Secret of the Polyglot
Okay, I don't know how they did this one.  But essentially there are two files in one: a PDF and a PNG.  If you open the PDF, you get one half, then if you open the PNG, you get the other piece.  I'm assuming because after the **IEND** for the PNG, there is extra data for a PDF.  So the header looks like a PNG, but there's data for a PNG *and* and PDF.  Cool.  flag is -> `picoCTF{f1u3n7_1n_pn9_&_pdf_724b1287}`

### Blast from the past
Lots of trial and error.  Basically, it comes down to a combination of a hex editor (`ghex` in my case) and `exiftool`.  Bard *almost* had it right with the following command `exiftool "-allDates<1970:01:01 00:00:00 -TimeZoneOffset=+00:00" your_image.jpg`, except it should be a `=` instead of a `<` for the allDates.  Flag -> picoCTF{71m3_7r4v311ng_p1c7ur3_a25174ab}

## Binary Exploitation

### heap 0
Kept writing to buffer until I could inject data into the safe variable.  I wrote `abcdefghijklmnopqrstuvwxyzabcdefgh` to get to the flag.  Flag -> picoCTF{my_first_heap_overflow_c3935a08}

### heap 1
This one is a little different.  You have to write something to the address space where `safe_var` is stored.  It took a lot of guesswork, but I realized I was wrong about trying to force 64 characters into the program.  I tried 32 A's followed by a pico and got it to overwrite that address.  pico now equaled pico and the flag was printed.  picoCTF{starting_to_get_the_hang_ce5bee9b}
