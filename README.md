````Our once-venerable president has committed the unspeakable crime of dine-and-dashing the pizza during our own club meetings. He's on the run as we speak, but we're not sure where he's headed.

Luckily, he forgot that we had planted a packet sniffer on his laptop, and we were able to retrieve the following capture when we raided his apartment:

https://storage.googleapis.com/utctf/capture.pcapng

He's too smart to email his plans to himself, but I'm certain he took them with him somehow. Can you help us figure out which country he's fleeing to?
````

This challenge consisted of a PCAP containing a large amount of USB packets.
[Wireshark](/img/wireshark.png)
This writeup describes in detail how to extract
these keystrokes from the file: url

After following the steps to get the keystrokes extracted, I ran a slightly modified version of the script shown in the linked
writeup.

````
newmap = {
 2: "?",
 4: "a",
 5: "b",
 6: "c",
 7: "d",
 8: "e",
 9: "f",
 10: "g",
 11: "h",
 12: "i",
 13: "j",
 14: "k",
 15: "l",
 16: "m",
 17: "n",
 18: "o",
 19: "p",
 20: "q",
 21: "r",
 22: "s",
 23: "t",
 24: "u",
 25: "v",
 26: "w",
 27: "x",
 28: "y",
 29: "z",
 30: "1",
 31: "2",
 32: "3",
 33: "4",
 34: "5",
 35: "6",
 36: "7",
 37: "8",
 38: "9",
 39: "0",
 40: "Enter",
 41: "esc",
 42: "del",
 43: "tab",
 44: " ",
 45: "-",
 47: "[",
 48: "]",
 55: ".",
 56: "/",
 57: "CapsLock",
 79: "RightArrow",
 80: "LetfArrow"
 }

myKeys = open('hexoutput.txt')
i = 1
for line in myKeys:
    bytesArray = bytearray.fromhex(line.strip())
 #print "Line Number: " + str(i)
    for byte in bytesArray:
        if byte != 0:
            keyVal = int(byte)
 
            if keyVal in newmap:
                print newmap[keyVal]
            else:
                print "No map found for this value: " + str(keyVal)
 
    i+=1
````
after running the script and replacing newline chars with spaces, I got the following output:

`g p g g     - c   f f l l a a g g s g s . p p n n g Enter u t ? ? n ? ? o ? ? t ? f l a g ? ? [ ? t r y ? ? - ? h a a r r d e e r r ? ? ] ? Enter u t ? ? n ? ? o ? ? t ? f l a g ? ? [ ? t r y ? ? - ? h a r d e e r r ? ? ] ? Enter c p   f l a g g s s . p n g . g p g   / m e d i a / u s s e e r e r / ? ? u ? ? s ? ? b ? / Enter`

After removing dupicate characters and figuring out that consecutive question marks corresponds to the shift key being pressed, 
I was able to deduce what was being ran, the important parts being:
`gpg -c flags.png
utNOTflag{try_harder}`

So now I had to find a GPG file in the pcap and decode it with the discovered password. Finding the GPG file wasn't difficult
since it was the largest packet in the pcap:

After extracting the gpg file and running the command, I was able to decode the message:

It's a file. After redirecting the decoded message to an empty file and running `file` on it, I was able to determine it was a 
PNG. Opening it revealed the following:

Which is not very useful, so I opened it up with stegsolve.jar and started flipping through different panes until finding:

