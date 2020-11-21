# Sometimes Simpler is Better

**Category**: DFIR \
**Points**: 800 
>Description: \
>You have been provided a basic pcap with some encoded data, can you figure out what is there? \
>PCAPHERE

We are given a pcap file to examine, lets take a look in wireshark: \
\
<img src=https://user-images.githubusercontent.com/74765175/99862400-77692880-2bfe-11eb-960a-43015cab7129.png width=75% height=75%>\
\
Yes we have some packets, only 7 though so not much to work with. Let's check out the TCP streams.\
<img src=https://user-images.githubusercontent.com/74765175/99862549-0413e680-2bff-11eb-837e-6e0580267311.png width=50% height=50%>\
\
Ok only one stream, the only data in here is non printable ASCII. Let's check this out in RAW form: \
<img src=https://user-images.githubusercontent.com/74765175/99862659-71c01280-2bff-11eb-9ef7-064f1df4411d.png width=50% height=50%>\
\
Ok we have some text, looks to be hex. Let's see what the Chef thinks about it:
```
ccd8c2cef6dee4c8d2dcc2d8e6fa
```
<img src=https://user-images.githubusercontent.com/74765175/99862836-2ce8ab80-2c00-11eb-9035-806373e35564.png width=50% height=50%>\
After putting in the known plaintext of flag and ticking intensive mode we are rewarded with our flag\
```
flag{ordinals}
```
