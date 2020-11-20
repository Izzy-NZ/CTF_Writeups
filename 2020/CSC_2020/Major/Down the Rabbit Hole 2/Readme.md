# Down the Rabbit Hole 2

**Category**: Crypto \
**Points**: 500 \
>Description: \
>Files in files in files in files in files in files in files
>
>The flag is not in standard format and will need to be wrapped in FLAG{XXX} for submission.
>
><img src=https://user-images.githubusercontent.com/74765175/99828808-4ec23e00-2bc0-11eb-86c5-00c59c7a9a19.jpg width=25% height=25% alt=Down_the_rabbit_hole_2.jpg>

Seems like a Stego challenge, let's see what could be hidden in here:\
I first noticed the thumbnail when viewing in kali's file manager had some text that wasn't in the original image:\
\
<img src=https://user-images.githubusercontent.com/74765175/99830035-fd1ab300-2bc1-11eb-9fa0-137d0cca45ec.png width=35% height=35% alt=Different Thumnail Image>
```
backwardsisforwards
```
Not the flag but let's put that aside for later and try strings on the file:
```
kali@kali:~/Documents/Down_the_rabbit_hole_2$ strings Down_the_rabbit_hole_2.jpg
S1Ir
I.>H)a
& c[
\ZH[7U
D4      Y
]w@&
'b<     :
"*PK    <---!!!
BQ\4
rabbit_hole.txt   <---!!!
kali@kali:~/Documents/Down_the_rabbit_hole_2$ 
```
We have a potential zip file signature and a reference to a .txt file\
Let's try and unzip this:
```
kali@kali:~/Documents/Down_the_rabbit_hole_2$ 7z e Down_the_rabbit_hole_2.jpg

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.utf8,Utf16=on,HugeFiles=on,64 bits,4 CPUs Intel(R) Core(TM) i9-9900K CPU @ 3.60GHz (906EC),ASM,AES-NI)

Scanning the drive for archives:
1 file, 2072312 bytes (2024 KiB)

Extracting archive: Down_the_rabbit_hole_2.jpg
--
Path = Down_the_rabbit_hole_2.jpg
Type = zip
Offset = 1933578
Physical Size = 138734

    
Enter password (will not be echoed):
```
Looks like we need a password, will try that thumbnail text from earlier (backwardsisforwards)
```
Enter password (will not be echoed):
Everything is Ok      

Size:       570564
Compressed: 2072312
kali@kali:~/Documents/Down_the_rabbit_hole_2$ ls
Down_the_rabbit_hole_2.jpg  rabbit_hole.txt
kali@kali:~/Documents/Down_the_rabbit_hole_2$ 
```
Success, this text file is one very long string, possibly encoded let's see what the chef can do:\
<img src=https://user-images.githubusercontent.com/74765175/99838335-d95d6a00-2bcd-11eb-976f-5645cdb07313.png width=35% height=35%>\
Nothing automated but looking at the start of this string we would usually see an equals sign like this
at the end of a base64 encoded string as padding, thinking back to the message in the thumbnail image
maybe we need to reverse the string:
<img src=https://user-images.githubusercontent.com/74765175/99838769-80420600-2bce-11eb-963f-2607ff3ebe52.png width=55% height=55%>\
Ok so we have a php file now, seems to be extracts from the Alice in Wonderland book, with some hex encoded and octal encoded strings
randomly jumbled up, maybe some sort of php code obfuscation. A particularily long string appears in the file so let's focus on that first:\
<img src=https://user-images.githubusercontent.com/74765175/99845013-d6b44200-2bd8-11eb-91cc-43026c91a324.png width=55% height=55%>\
https://www.unphp.net/ is a site that can decode obfuscated code for us, simply paste the string in and let the site do the work.\
<img src=https://user-images.githubusercontent.com/74765175/99840135-d44dea00-2bd0-11eb-8014-73f9694155eb.png width=55% height=55%>\
Looks like hex, let's go back to the chef and see what this new string is hiding:\
<img src=https://user-images.githubusercontent.com/74765175/99840338-3c043500-2bd1-11eb-9265-5d02216fc6dc.png width=55% height=55%>\
A 7zip file, let's save it and see if we can unzip it:\
```
kali@kali:~/Documents/Down_the_rabbit_hole_2$ 7z e php.7z -o./php

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=en_US.utf8,Utf16=on,HugeFiles=on,64 bits,4 CPUs Intel(R) Core(TM) i9-9900K CPU @ 3.60GHz (906EC),ASM,AES-NI)

Scanning the drive for archives:
1 file, 57253 bytes (56 KiB)

Extracting archive: php.7z
--
Path = php.7z
Type = 7z
Physical Size = 57253
Headers Size = 138
Method = LZMA2:768k
Solid = -
Blocks = 1

Everything is Ok

Size:       724992
Compressed: 57253
kali@kali:~/Documents/Down_the_rabbit_hole_2$ cd php
kali@kali:~/Documents/Down_the_rabbit_hole_2/php$ ls
birthday_cake.db
kali@kali:~/Documents/Down_the_rabbit_hole_2/php$ file birthday_cake.db 
birthday_cake.db: SQLite 3.x database, last written using SQLite version 3032002
kali@kali:~/Documents/Down_the_rabbit_hole_2/php$ 
```
Success we now have a database file to work with/
Kali has an inbuilt DB browser we can use to view/
<img src=https://user-images.githubusercontent.com/74765175/99841116-8b973080-2bd2-11eb-880e-66ff6a428a79.png width=55% height=55%>\
We have a cake table with 2 columns: layer and cake. The cake column appears to be a long hex string.\
Maybe we have to combine the layers of the cake, we will filter by layer and start with layer one copy\
pasting into a new text file:\
<img src=https://user-images.githubusercontent.com/74765175/99841600-50e1c800-2bd3-11eb-9642-dd7c645310a2.png width=55% height=55%>\
The chef detects this as a tiff file so let's save and examine:\
<img src=https://user-images.githubusercontent.com/74765175/99842380-95219800-2bd4-11eb-9952-b5b47a31a22e.png width=55% height=55%>\
Oh dear we appear to have a QR code puzzle let;s see if we can assemble the whole image.\
Stegsolve.jar can do this for us:\
<img src=https://user-images.githubusercontent.com/74765175/99842587-fba6b600-2bd4-11eb-9c50-b1fb2eb7f3af.png width=55% height=55%>\
Examining any of the color planes gives us the whole QR code so we can save and scan online or with you phone.\
I used https://zxing.org/w/decode.jspx \
<img src=https://user-images.githubusercontent.com/74765175/99842865-75d73a80-2bd5-11eb-8dae-cfdacd498e09.png width=55% height=55%>\
```
425a6839314159265359c790c58100005887803ffffff03fefdfe05003fa0027a7b2b359ac34c42689480000000068600d343468c46403400686090535511a686234c2180320009aa550640026000462600052953d293c53d40069900064327a87987f7a436c2904360dbd86ccc78d4c7131d0f21a1b8860df6b1f2017e761593ab08e04d320967b58173b3c9d345cbd07c6cc040b06f634c0041dc4a201624ba31a66aa44b241fb552ad1151688160e8b0e0ad872738472c5ff5b83b06693085a083a0ca65031bdd751d0566975877a720539c5d6cc6b3591b30ed01260c015ae24744530ca585e2c080c3462f6563d4a8316678353d6a097accececbaa141b18c48e4847b0ab23aba2e52440ce837b2a666a650ac1545940c682850e986285112448eab61d9e21d856c15255c4eb68d81ba1326253646070c4e162945e59ea58a20d8081043e1512483d167ac135430cd554c4876708a7b62f5ad07449315c690c833573c90aef4352716e74581c0e10fd247ab7a3d032e2b8d63adb2623598b5a64668ab01960164501866a5d5d6606419818ec1d9da85b521f45e4a38137d4b950e29650e747541c88fd884d1ee1846406fddc908406ad8c62a0ca0c60c95daac887226525641cb385203d52036a686326563333318cb333807525a68dc3449c4a7e5be4f655683c52f511ef27749e983a64e6977a71272a322e21da1d953b68eba5fe4b4c6fd5692ba52e81d81d14ba54d01f523a24d55b06d4692e8ac7625f397783483fdc4818be38001b91423ac6c61f09e952c2fd1385d61a60e2ca4d62ab1a2b45985b435756e1a3687d1fd979d56fd1ec3949f12651bd36e95babf4711aac7616901858db1109064ad10752b7356eddaccd3735bb5c28ee43fb279a4f0137878cae1473a3a64d8d56318c666618b30cb198cc6336d2c1e12f9a3547d957da9f8341360989707243f10d95b15b6d8c658ccc66618db6c69313f9177245385090c790c581
```
Another hex string; back to the chef.\
<img src=https://user-images.githubusercontent.com/74765175/99843100-dc5c5880-2bd5-11eb-9e30-0f67cd767468.png width=55% height=55%>\
Converting from hex and the bzip2 decompressing gives us a string of phonetic alphabet/numbers.\
```
FourKiloAlphaJulietYankeeVictorThreePapaOscarVictorWhiskeyGolfIndiaIndiaDeltaZuluNovemberFiveTwoSierraAlphaFiveDeltaFoxtrotNovemberRomeoWhiskeyCharlieAlphaThreeLimaFoxtrotFoxtrotQuebecQuebecHotelAlphaThreeDeltaFoxtrotMikeFoxtrotZuluWhiskeyKiloLimaBravoAlphaOscarFiveUniformGolfSierraYankeeThreeIndiaEchoBravoThreeWhiskeyCharlieSixJulietAlphaJulietEchoQuebecGolfSixFiveLimaHotelNovemberBravoTwoCharlieAlphaFiveDeltaPapaEchoBravoTangoWhiskeySixIndiaDeltaGolfOscarJulietXrayWhiskeyTwoIndiaDeltaIndiaMikeVictorZuluGolfKiloPapaSevenCharlieQuebecCharlieOscarQuebecVictorYankeeUniformAlphaTangoRomeoKiloGolfQuebecYankeeLimaUniformEchoBravoSierraGolfKiloFourDeltaFoxtrotNovemberZuluSierraHotelGolfIndiaDeltaBravoEchoBravoTangoWhiskeySixThreeThreeEchoEchoBravoSierraGolfKiloYankeeLimaMikeEchoBravoXrayWhiskeyFourIndiaDeltaXrayNovemberBravoSierraXrayEchoZuluJulietAlphaPapaFoxtrotXrayXrayKiloIndiaDeltaXrayMikeFoxtrotXrayHotelIndiaIndiaDeltaUniformNovemberFourQuebecGolfOscarZuluLimaUniformEchoBravoTwoGolfSixLimaHotelCharlieQuebecCharlieOscarSierraAlphaFourThreeBravoNovemberFoxtrotSierraCharlieAlphaFiveDeltaIndiaMikeUniformQuebecEchoGolfYankeeLimaUniformFoxtrotYankeeFoxtrotOscarFoxtrotAlphaEchoFourJulietEchoQuebecGolfIndiaThreeThreeOscarFourKiloAlphaJulietSierraFiveBravoAlphaNovemberVictorTwoWhiskeyGolfTwoBravoAlphaMikeNovemberQuebecXrayEchoZuluJulietAlphaOscarFiveUniformGolfKiloFourTangoFoxtrotFourKiloAlphaJulietHotelYankeeUniformAlphaTangoUniformQuebecHotelGolfYankeeLimaJulietMikeQuebecQuebecEchoCharlieThreeDeltaJulietMikeNovemberSierraSierraFourCharlieXrayCharlieQuebecCharlieOscarFoxtrotIndiaTwoDeltaFoxtrotNovemberYankeeQuebecGolfSierraFiveBravoAlphaMikeRomeoXrayWhiskeyKiloFourThreeOscarFourKiloAlphaJulietSierraFiveBravoAlphaNovemberVictorQuebecXrayIndiaFiveDeltaFoxtrotOscarIndiaQuebecHotelOscarTwoDeltaJulietMikeNovemberUniformCharlieAlphaFiveThreeBravoPapaEchoQuebecHotelSierraThreeThreeVictorEchoBravoTangoWhiskeySixLimaHotelCharlieQuebecCharlieOscarSierraAlphaFourThreeBravoNovemberFoxtrotSierraCharlieAlphaFiveDeltaIndiaMikeUniformQuebecEchoGolfYankeeLimaUniformFoxtrotYankeeFoxtrotOscarFoxtrotAlphaEchoFourFourKiloAlphaJulietGolfFourThreePapaEchoBravoWhiskeyGolfSixThreeTangoHotelEchoBravoQuebecXrayGolfIndiaCharlieJulietEchoBravoTangoWhiskeyKiloFiveBravoAlphaKiloNovemberHotelUniformTwoRomeoKiloXrayJulietBravoCharlieVictorEchoRomeoJulietMikeFourKiloAlphaJulietTwoIndiaCharlieBravoNovemberRomeoUniformWhiskeyGolfZuluJulietAlphaMikeFoxtrotSierraGolfIndiaZuluLimaEchoEchoBravoQuebecXrayGolfIndiaDeltaBravoNovemberYankeeQuebecGolfKiloSixDeltaQuebecNovemberRomeoQuebecWhiskeyFourYankeeLimaUniformNovemberFoxtrotXrayWhiskeyFourLimaQuebecKiloFourKiloAlphaJulietYankeeTangoThreeIndiaFoxtrotQuebecQuebecHotelSierraThreeThreeVictorFourKiloAlphaJulietSierraFourTangoFoxtrotEchoBravoZuluXrayKiloFourTangoFoxtrotEchoBravoTwoGolfSixIndiaDeltaEchoNovemberFourQuebecHotelIndiaTwoDeltaBravoOscarQuebecWhiskeyOscarFoxtrotAlphaEchoFiveEchoBravoZuluWhiskeyCharlieTwoLimaEchoEchoBravoTwoGolfQuebecZuluJulietAlphaIndiaNovemberQuebecXrayIndiaLimaBravoAlphaFourKiloAlphaJulietYankeeZuluTangoMikeMikeFoxtrotTangoXrayWhiskeyTwoLimaGolfLimaFiveFourWhiskeySixFiveJulietNovemberNovemberFiveXrayGolfYankeeSixJulietOscarOscarFiveQuebecWhiskeyYankeeTwoTwoSevenNovemberQuebecYankeeGolfFourZuluZuluNovemberMikeVictorXrayGolfSixFiveLimaHotelNovemberBravoSixSixFoxtrotAlphaEchoFive
```
We can use https://www.dcode.fr/nato-phonetic-alphabet to quickly decode this:\
```
4KAJYV3POVWGIIDZN52SA5DFNRWCA3LFFQQHA3DFMFZWKLBAO5UGSY3IEB3WC6JAJEQG65LHNB2CA5DPEBTW6IDGOJXW2IDIMVZGKP7CQCOQVYUATRKGQYLUEBSGK4DFNZSHGIDBEBTW633EEBSGKYLMEBXW4IDXNBSXEZJAPFXXKIDXMFXHIIDUN4QGOZLUEB2G6LHCQCOSA43BNFSCA5DIMUQEGYLUFYFOFAE4JEQGI33O4KAJS5BANV2WG2BAMNQXEZJAO5UGK4TF4KAJHYUATUQHGYLJMQQEC3DJMNSS4CXCQCOFI2DFNYQGS5BAMRXWK43O4KAJS5BANVQXI5DFOIQHO2DJMNUCA53BPEQHS33VEBTW6LHCQCOSA43BNFSCA5DIMUQEGYLUFYFOFAE44KAJG43PEBWG63THEBQXGICJEBTWK5BAKNHU2RKXJBCVERJM4KAJ2ICBNRUWGZJAMFSGIZLEEBQXGIDBNYQGK6DQNRQW4YLUNFXW4LQK4KAJYT3IFQQHS33V4KAJS4TFEBZXK4TFEB2G6IDEN4QHI2DBOQWOFAE5EBZWC2LEEB2GQZJAINQXILBA4KAJYZTMMFTXW2LGL54W65JNN5XGY6JOO5QWY227NQYG4ZZNMVXG65LHNB66FAE5
```
Cyberchef tells us this is Base32 encoded string:\
<img src=https://user-images.githubusercontent.com/74765175/99843712-db77f680-2bd6-11eb-8f41-4b68d5f85845.png width=55% height=55%>\
```
“Would you tell me, please, which way I ought to go from here?”
“That depends a good deal on where you want to get to,” said the Cat.
“I don’t much care where–” said Alice.
“Then it doesn’t matter which way you go,” said the Cat.
“–so long as I get SOMEWHERE,” Alice added as an explanation.
“Oh, you’re sure to do that,” said the Cat, “flag{if_you-only.walk_l0ng-enough}”
```
There we have the flag:
```
flag{if_you-only.walk_l0ng-enough}
```
