g p g g     - c   f f l l a a g g s g s . p p n n g Enter u t ? ? n ? ? o ? ? t ? f l a g ? ? [ ? t r y ? ? - ? h a a r r d e e r r ? ? ] ? Enter u t ? ? n ? ? o ? ? t ? f l a g ? ? [ ? t r y ? ? - ? h a r d e e r r ? ? ] ? Enter c p   f l a g g s s . p n g . g p g   / m e d i a / u s s e e r e r / ? ? u ? ? s ? ? b ? / Enter

gpg -c flags.png
utNOTflag{try_harder}
newmap = {
 2: "PostFail",
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
 44: "space",
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

after formatting the output file a bit (changing PostFail to ?, space to ' ', and getting rid of newline chars)
