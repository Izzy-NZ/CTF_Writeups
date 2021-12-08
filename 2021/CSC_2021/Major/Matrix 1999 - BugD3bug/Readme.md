# Matrix 1999 - BugD3bug

>Description: \
>I've already decompiled the APK file for you. However I can't find my flag inside. Can you help?flag format: flag{text_goes_here}

Needle in a haystack here TBH i got lucky and found the hidden text file on my first click through:
```
..\D3bugg3r\sources\com\example\ctf\test\test\test.zip\test\test\test.zip\test\test\test.zip\test\test\.hidden.txt
```
At the bottom of .hidden .txt is a hex encoded / reversed flag:
<img src=https://user-images.githubusercontent.com/74765175/145141623-1f1a867c-faf7-4a9d-8e1b-f773844f9274.png width=75% height=75% alt=Different Thumnail Image> 
```
flag{hello_world_flag}
```
