## Sc 01 Logview
description: The Professor's log viewer is a clean little internal tool… until you notice it can be tricked into reading arbitrary files. Patch the path handling to lock it to the logs directory, then claim the vault key.

the website was a log viewer and we had a few options, one of which would patch the existing 

after a bit of digging around, i found that the server.js and safePath.js was public under the endpoint /source

this made me realize that i can change the safePath.js to a file that would run to output me the flag file that was stored in the enviorenment variable. 

so rather than taking the right path, i submitted the code for the safePath.js file which would output an error and print the flag and key to me. 

i asked gpt to give me the code because i was running low on time and it gave me the payload and i got the flag this way.

FLAG: `TDHCTF{BELLA_CIAO_NO_MORE_DOT_DOT_SLASH}`
KEY: `69afc9eac440d6d06ba9307abbad69b437eaf0cbcce509146c1e785b67505cb4`