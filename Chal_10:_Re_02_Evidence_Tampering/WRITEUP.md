## Re 02 Evidence Tampering

Similar to the Re 01 CTF, this had a binary given to us probably for reverse engineering and we had to find the flag. 

binary was `evidence_tool` and similar to Re 01, this one did the same kind of thing when you decompile the binary or when you use strings on the bin. 

        Timeline rewrite validated.
        127.0.0.1
        {"timestamp":%llu}
        "key":"
        "flag":"
        Key: %s
        Flag: %s
        Rejected: timestamp mismatch.
        === Evidence Tampering Console ===
        POST /validate.php HTTP/1.1
        Host: localhost:31337
        Content-Type: application/json
        Content-Length: %zu
        Server connection failed. Run inside container.
        Make sure Apache is running on localhost:31337
        j)CbE2:
        9[MM2
        ;*3$"
        GCC: (Debian 12.2.0-14+deb12u1) 12.2.0
        .shstrtab
        .interp
        .note.gnu.property
        .note.ABI-tag


here is a small output of the strings on the bin. 

this just made me quickly connect to the ssh and check the run the find command similar to what i did in the Re 01, here is the command: `find / -name validate.php 2>/dev/null` and sure enough, i found the file, the key and the flag. 

FLAG: `TDHCTF{tampered_time_offset}`
KEY: `49ffbabbc5429e5204def805fd891850bbd6496243a64a9e348d78f2a4d74543denver`