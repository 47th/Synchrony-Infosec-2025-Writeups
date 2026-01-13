## CRYPTO 01: INTERCEPTED COMMS

description: An operative's encrypted notes use a weak cipher. Decrypting them reveals internal codenames for A₀ submodules.
files: intercepted_message.txt

intercepted_message.txt
> === VAGREPRCGRQ GENAFZVFFVBA ===
SEBZ: HAXABJA BCRENGVIR
GB: URVFG PBBEQVANGBE
FGNGHF: RAPELCGRQ
>
> ZRFFNTR:
Cebsrffbe, V'ir frpherq gur vagry hfvat bhe fgnaqneq cebgbpby - gur fnzr zrgubq jr hfrq sbe gur Eblny Zvag oyhrcevagf. Rnpu cvrpr bs vasbezngvba vf ybpxrq va oybpxf bs fvkgrra, punvarq gbtrgure yvxr gur inhyg qbbef ng gur Onax bs Fcnva. Abguvat fgnaqf nybar - rirel oybpx qrcraqf ba jung pnzr orsber vg.
>
> Gur vavgvnyvmngvba frdhrapr fgnegf sebz mreb - n pyrna fyngr, fvkgrra mrebf gb ortva gur punva. Guvf vf ubj jr'ir nyjnlf qbar vg, Cebsrffbe. Fgnaqneq cnqqvat nccyvrq, whfg yvxr lbh gnhtug hf.
>
> Gur xrl gb haybpx guvf vf: URVFGStwKorMmAx6
Erzrzore, vg zhfg or rknpgyl fvkgrra punenpgref - ab zber, ab yrff. Gung'f gur fvmr bs bhe oybpxf, Cebsrffbe. Bar uhaqerq gjragl-rvtug ovgf cre oybpx, fvkgrra olgrf rnpu.
>
> Gur cnlybnq orybj unf orra rapbqrq hfvat bhe onfr genafzvffvba sbezng - lbh'yy arrq gb qrpbqr vg svefg orsber nccylvat gur qrpelcgvba xrl. Guvax bs vg yvxr gur Cebsrffbe'f cyna: svefg lbh qrpbqr gur zrffntr, gura lbh oernx gur pvcure.
>
> Gur pevgvpny vasbezngvba vf ybpxrq vafvqr. Hfr gur xrl nobir jvgu gur mreb vavgvnyvmngvba frdhrapr gb erirny jung jr'ir qvfpbirerq nobhg gur Qverpgbengr'f bcrengvbaf.
>
> RAPELCGRQ CNLYBNQ:
QZXvlTWfSR0SNB5yY70Y2d0YswlOC7FyhlGZauag/YFXBnsBN67FyArkFH2AQ2zcvsJDzVk0h6hAlJREn1qiwaSfX0yncSTaxerwnMWKJnqfmi8H94ifCH5AqXms2Sk6Uc4ydNORnNhbPBfyZXnQ97Kp7+jVQ1hZ3XHNtWnf5pHZQITtU5/L/lboKdcgRWB/
>
> Erzrzore: qrpbqr svefg, gura qrpelcg. Gur gehgu vf ybpxrq va gubfr oybpxf, Cebsrffbe.
>
> RAQ GENAFZVFFVBA


this is clearly encrypted using some kind of cipher, i tried ceasar cipher and some other popular ones but had no luck, even tried cipher identifiers but no luck, and everytime cipher identifier cannot detect a cipher, it is most probably ROT13 and bingo, its ROT13

this is what the message says after being decrypted

>=== INTERCEPTED TRANSMISSION ===
FROM: UNKNOWN OPERATIVE
TO: HEIST COORDINATOR
STATUS: ENCRYPTED
>
>MESSAGE:
Professor, I've secured the intel using our standard protocol - the same method we used for the Royal Mint blueprints. Each piece of information is locked in blocks of sixteen, chained together like the vault doors at the Bank of Spain. Nothing stands alone - every block depends on what came before it.
>
>The initialization sequence starts from zero - a clean slate, sixteen zeros to begin the chain. This is how we've always done it, Professor. Standard padding applied, just like you taught us.
>
>The key to unlock this is: HEISTFgjXbeZzNk6
Remember, it must be exactly sixteen characters - no more, no less. That's the size of our blocks, Professor. One hundred twenty-eight bits per block, sixteen bytes each.
>
>The payload below has been encoded using our base transmission format - you'll need to decode it first before applying the decryption key. Think of it like the Professor's plan: first you decode the message, then you break the cipher.
>
>The critical information is locked inside. Use the key above with the zero initialization sequence to reveal what we've discovered about the Directorate's operations.
>
>ENCRYPTED PAYLOAD:
DMKiyGJsFE0FAO5lL70L2q0LfjyBP7SluyTMnhnt/LSKOafOA67SlNexSU2ND2mpifWQmIx0u6uNyWERa1dvjnFsK0lapFGnkrejaZJXWadszv8U94vsPU5NdKzf2Fx6Hp4lqABEaAuoCOslMKaD97Xc7+wID1uM3KUAgJas5cUMDVGgH5/Y/yobXqptEJO/
>
>Remember: decode first, then decrypt. The truth is locked in those blocks, Professor.
>
>END TRANSMISSION

the message says that the given payload has to be first decoded using the "base transmission format" which hints to base64 encoding and then decrypted using the key `HEISTFgjXbeZzNk6` and the initial sequence starting from 16 zeros of the chain. this hints to the aes 128 bit encryption and no doubt it gives some data encoded in hex. 

`4e6d4e6a4d6a4a694e7a4a6c4d6d4d77596a526a4f47526d4f54686b5a5455344f5751785a6d526c4e6d566d4f54646d4e5467344f54497a4d7a4d774d7a4d795a5464684d5449774e5759345a6a49344e444e694d413d3d0a564552495131524765326c7564475679593256776447566b58324e766257317a5832526c59334a356348526c5a48303d`

we get the following when decoded : 
`NmNjMjJiNzJlMmMwYjRjOGRmOThkZTU4OWQxZmRlNmVmOTdmNTg4OTIzMzMwMzMyZTdhMTIwNWY4ZjI4NDNiMA==
VERIQ1RGe2ludGVyY2VwdGVkX2NvbW1zX2RlY3J5cHRlZH0=`

this is encoded further in base64 which when decoded gives us the key and the flag

key: `6cc22b72e2c0b4c8df98de589d1fde6ef97f588923330332e7a1205f8f2843b0`
flag: `TDHCTF{intercepted_comms_decrypted}`