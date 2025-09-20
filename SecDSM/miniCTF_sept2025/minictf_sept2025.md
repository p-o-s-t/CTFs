# SecDSM MiniCTF for September 2025
## Deets

Name: air gapped

Author: Coop3r

Link: https://minictf.secdsm.org/airgapped/

## Rules
- There are 3 flags total.
- Standard flag format: SecDSM{flag}
- DM flags to Coop3r.

## Walkthrough
For this MiniCTF, we're provided with a packet capture (pcap) that will lead us to 3 different flags.  As with any challenge that has multiple flags in one file, we may jump around to find the flags in an unusual order.  This write-up starts with Flag #1.

### Flag 1
The pcap file isn't large at 127kB, so I use Wireshark to inspect the contents of the pcap.   A quick check of the Protocol Hierarchy Stats shows that we only have a few protocols to dig into.

![Protocol Hierarchy Statistics from the MiniCTF pcap](image.png)

There's only one UDP stream, so we open that up to immediately some login attempts that eventually up being successful.  

![alt text](image-1.png)

At first glance- and based on the rules- we see that **SecDSM{let_me_in}** is very likely to be our first flag.  However, before I tried to slide into Coop3r's DMs with this finding, I noticed that it was followed by `Login incorrect` when that is entered.  But a successful login does occur sometime before Frame 235, when the ctrlX CORE logo appears using ASCII.  

Looking between frames 177 and 235, I noticed that there were single characters that matched the original flag, but with some small differences.  With the display filter `ip.src == 172.28.173.108 && (frame.number >=177 && frame.number <= 235)`, I found that some of the characters were actually capitalized.  This was seen as I scrolled down through each of the packets.  

With that, we get a positive confirmation from the man, the myth, the legend, Coop3r that **Flag 1 = SecDSM{Let_Me_In}**.  1 down, 2 to go.

### Flag 3
I don't remember the exact reason, but my instincts told me to jump to the end of the pcap to get an idea of what may have happened after as a result of the login and following actions on the possibly compromised device.  With mentions of `Erasing command history buffer` and `All traces removed` near the end of the pcap, it lead me to think that some kind of automated script was ran on the device.  Something to keep in the back of my mind as I continued to work my way backwards in the timeline.

![Working my way backwards in the pcap](working_backwards.png)

As I continue, I finally come across very apparent use of base64 encoding for some purpose.  It appears that some data was likely exfil'd off this device from a file called `secrets`.  The script pulled whatever was in the `secrets` file with the command line: `dd if=/dev/secrets | gzip | base64`.  This told us 3 things:
- The contents of the file were of interest
- GZip compression was used to create an archive
- The archive was base64 encoded

To pull the base64 encoding out of the pcap, I went to the command line and used *tshark* to grab the  data from frames 1189 to 1211 using `tshark -n -r ctf-2025-09.pcap -Y "(frame.number>=1189 && frame.number<=1211) && ip.src==10.200.138.212" -T fields -e data`.  With a little bit of cleanup to get rid of some of the data at the beginning and end- like the transfer speed and the console popping back up- I popped the hex encoded data into CyberChef.  With the following [recipe](https://gchq.github.io/CyberChef/#recipe=Find_/_Replace(%7B'option':'Regex','string':'%5E%5C%5Cd.%5C%5Cd%5C%5Cd'%7D,'',true,false,true,false)Find_/_Replace(%7B'option':'Regex','string':'0d0a'%7D,'',true,false,true,false)Remove_whitespace(true,true,true,true,true,false)From_Hex('Auto')From_Base64('A-Za-z0-9%2B/%3D',true,false)Gunzip()), I was able to discover the contents of the secrets file:

![Contents of the secrets file after being decoded through Cyberchef](secrets_file_contents.png)

Why, these look like hashes!  So the next step to find flag 3 was to probably to do some kind of  password cracking.  And I'll admit, I did try to foolishly crack these hashes with absolute *no insight* if that was even the right thing to do.  I definitely wasted a good chunk of time trying to find the original values for the message digest hash values, with- as you might guess- zero success.

After stepping away for about an hour, I came back to the contents of the file to look at what was unusual.  There had to be something that stood out and for sure, one of the entries was different than the others:

**25:J9:$9$7vV2oDjqf5F9AMLxdY29ApuRSdVYGDkreb24oji69ApRSdbYoZjKMX-bwJZHqmPF/tu1SeW**

A [quick search](https://duckduckgo.com/?t=lm&q=%25249%2524+hash+prefix) told me this was the Type 9 hash used for Juniper OS.  Using my biggest of brains, I did another search by adding `decode` to the end which lead me to the extremely helpful website https://www.m00nie.com/juniper-type-9-password-tool/, which of course had a relevant meme right at the top.  

Another thumbs up emoji reaction in the SecDSM Discord tells me that **Flag 2 = SecDSM{too_many_secrets}** is correct.  2 down, hardest one to go. */me gulps*

## Flag 2
