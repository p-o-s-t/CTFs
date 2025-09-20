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

At first glance- and based on the rules- we see that `SecDSM{let_me_in}` is very likely to be our first flag.  However, before I tried to slide into Coop3r's DMs with this finding, I noticed that it was followed by `Login incorrect` when that is entered.  But a successful login does occur sometime before Frame 235, when the ctrlX CORE logo appears using ASCII.  

Looking between frames 177 and 235, I noticed that there were single characters that matched the original flag, but with some small differences.  With the display filter `ip.src == 172.28.173.108 && (frame.number >=177 && frame.number <= 235)`, I found that some of the characters were actually capitalized.  This was seen as I scrolled down through each of the packets.  

With that, we get that **Flag 1 = SecDSM{Let_Me_In}**.

