# Hackers 1994 - Intensified

>Description: \
>James got an zip file with a passphrase. Along with the zip file there is a music file listen to it and use it wisely. 

We are given two files: Intensified.zip and Intensified.wav \
Within Intensified.zip there is flag.txt however the zip is password protected \
Intensified.wav has nothing of interest in the strings however when played produces a series \
of beeps that sound like dialling on an old phone. \
Further research would indicate that these are DTMF tones, and with the proper decoder will produce \
a series of numbers. \
https://unframework.github.io/dtmf-detect/ is a useful site for this where you can upload a wav file \
to automatically decode: \
<img src=https://user-images.githubusercontent.com/74765175/145130153-3a656683-048d-4131-85aa-df9f5b67d605.png width=35% height=35% alt=Different Thumnail Image>
```
2462523123431
```
Using this string of text as the password for the zip file successfully gets us flag.txt:
```
The flag is encrypted its easy decrypt it...
 
MZWGCZ33IRKE2RS7JFXHIZLOONUWM2LFMRPWC5C7NF2HGX3QMVQWW7I=
```
CyberChef can work it's magic on this string which gives us a Base32 decoded text of: \
flag{DTMF_Intensified_at_its_peak}
