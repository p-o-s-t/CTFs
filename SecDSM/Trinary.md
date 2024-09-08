The September 2024 SecDSM MiniCTF, [Trinary](https://minictf.secdsm.org/Trinary/), is a sequel to the [Dark Matter](https://minictf.secdsm.org/DarkMatter/) that was published in June 2024.  In the Dark Matter miniCTF, participants had to decode a barcode that used the same [data encoding scheme](https://imgur.com/a/dark-matter-android-barcode-wo3K9) that was seen on the neck of [The Android](https://darkmatter.fandom.com/wiki/The_Android).  

However, this sequel comes with a colorful twist. Instead of just black and white, there is now 7 different colors present in the encoding scheme:
- Red
- Green
- Blue
- Cyan
- Yellow
- Purple
- White

![image](https://github.com/user-attachments/assets/0522e277-a0b1-4a96-beef-9e8c458055c8)

At the beginning, it appeared to me that the use of these colors appeared to be randomly applied throughout the majority of lines and blocks.  I knew they would play some role, but I didn't know what just yet.  Instead, I looked further into the possible clue from the name of the miniCTF, Trinary, and looked into [Ternary computers](https://en.wikipedia.org/wiki/Ternary_computer).  

After some skimming, I thought maybe the separation in the middle between the blocks was the 0, and the +/- 1 was above and below the line.  But soon realized that didn't fit the encoding scheme, so I stopped digging down that rabbit hole.  It took me about 20 minutes to realize I had veered way off-course.

I went back to just trying to apply what I already knew from the Dark Matter miniCTF.  The first 3 bytes colored in red, green, and blue ended up being 0x53, 0x65, and 0x63 respectively.  I threw these into [Cyberchef](https://gchq.github.io/CyberChef/) and got my first success:

![image](https://github.com/user-attachments/assets/8d29ec4a-5e8f-4219-9b54-676bb1ce64c1)

I then tried to do the same with various bytes in the provided image, but ended up with a lot of 0xFF, which didn't fit into the convention as the conversion from hex to ASCII didn't produce a human readable output.  I spent about 10 minutes trying this before giving up on that failed endeavor, but it raised a different question to pursue: how do I get the **DSM{** from the next 4 bytes to match what it says on the challenge page?

Suddenly, I had a flashback to a puzzle game that I played almost 8 years ago called [Zero Escape: Zero Time Dilemma](https://store.steampowered.com/app/311240/Zero_Escape_Zero_Time_Dilemma/).  In it, there was a series of puzzles that dealt with the application of color and color theory, one of which was the [RGB Color Model](https://en.wikipedia.org/wiki/RGB_color_model):

![image](https://github.com/user-attachments/assets/2fff4a10-18de-462b-b095-7d09cdc3ae54)

And suddenly it just clicked.  The blocks that had the colors of cyan, yellow, purple, or white were to highlight the existence of several blocks laid on top of each other.  But even though I now understood the color gimmick, I didn't know what exactly to do with this new knowledge. 

My first thought was to write 3 bytes in hexadecimal out by themselves.  For example, the 4th pair of blocks in the image would be 0x20 0x15 0x0F:

![image](https://github.com/user-attachments/assets/9b44aea3-f828-4f6a-b9de-854912901716)

Which is just garbo nonsense, as it's not human readable and doesn't really fit the convention introduced in the June miniCTF.  I tried it again with a few more pairs of blocks and kept getting nonsense outputs.  What I was doing was correct, but why wasn't it correct?  In frustration I looked back at the RGB color model, thinking it was to blame for leading me astray.  And that was when I had my second "A HA" moment.

When you have the colors of cyan, yellow, purple, or white, these are created by *adding* the 2 or 3 colors of red, green, and blue together.  So while I could find the 3 bytes in each colored block pair, I was applying them incorrectly.  I had to add them all up!  Time for a calculator that could add hex numbers together.

I didn't have one available and I was too lazy to look for one in the repositories for my distribution, so I used the Google search bar to do my maths! 😅  But my idea to try summarizing the colors was correct, as 0x20 + 0x15 + 0x0F = 0x44, which is equivalent to '**D**'.  

The next issue I ran into, but was solved rather easily, was any summations that ended up as something like 0x17D.  For sums like this, I just dropped the leftmost character (e.g., 0x17D becomes 0x7D) and got the byte that I needed.  I'm sure there is a better way to do this, but in the moment this was my quickest- albeit not cleanest- option.

After cranking out the sums for each pair of blocks, I eventually ended up with that flag of **SecDSM{Sum_of_Colors}**.
