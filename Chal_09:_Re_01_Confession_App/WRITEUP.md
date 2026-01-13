## RE 01 CONFESSION APP

we were given a binary confession_app and an ssh to a machine which had this binary.

i dont think i solved this challenge at all the way it was intended to lol, instead i found a cleaver shortcut to get the flag and the key. 

i decompiled the given binary and also tried to `strings confession_app` and noticed that what the binary does is, it boots up a new web server at the localhost:31337 and makes a `POST` request to the `\validate.php` endpoint which then returns the FLAG and the KEY. 

small output of using stirngs on the `confession_app`: 

        LD_LIBRARY_PATH
        /proc/self/status
        TracerPid:
        CHALLENGE_KEY
        127.0.0.1
        {"passphrase":"%s"}
        "key":"
        "flag":"
        POST /validate.php HTTP/1.1
        Host: localhost:31337
        Content-Type: application/json
        Content-Length: %zu
        Server connection failed. Run inside container.
        Make sure Apache is running on localhost:31337

since this is running on localhost, the files of the server should be somewhere on the machine itself, i tried to find it using the find tool on the comman line `find / -name validate.php 2>/dev/null`, turns out it was hiding in the `/var/www` folder, if i remember correctly along with the php file, a file with the key was present and the flag was hard coded in the validate.php file itself. 

FLAG: `TDHCTF{confession_gateway_phrase}`
KEY: `c3b125c65d5aeef443e412956c73e38bded330b3a026456b96beb2f5f4409ac4rio`