# Matrix 1999 - C00rupt3d

>Description: \
>You'll need to dig deep to find this oneflag format: flag{wordsgohere}

We are given CallMeX.wav and NOTE.txt. \
NOTE.txt appears to be a clue to the solution:
```
Lisa : What happened ?

Nakasoft : I am listening to a music but cannot figure out the name. Can you please help me ?

Lisa : But why you want to find the name ?

Nakasoft : Because the artist's name is the password for my confidential documents.

Lisa : Ohh okay, let me hear it once.

Lisa : Umm.. I hear it almost everyday but even I don't know the name.

Nakasoft : I hope if someone can help. :(
```
Then at the very bottom:
```
Author name in all CAPS
```
Well we can get the Author using Shazam: \
https://www.youtube.com/watch?v=LiqIQ5He7_4 \
RANDALL \
Now to get how they have hidden the confidential documents: \
A google search for Nakasoft comes up with a Xiao Steganography tool \
Using this tool we can extract three documents from the CallMeX.wav file using the \
password RANDALL: \
bmp.bmp \
jpg.jpg \
txt.txt \
Running strings on bmp.bmp gives us the flag: /
```
flag{Ext3ns1ons_aRe_A_Li3}
```
