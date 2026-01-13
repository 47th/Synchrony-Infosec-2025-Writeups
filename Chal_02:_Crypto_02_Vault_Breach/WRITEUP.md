## CRYPTO 02: Vault Breach

description: Lisbon identifies an AES-encrypted memo. Using known plaintext structures, the crew recovers a name: The Directorate's chief architect. They now know who built A₀.
files: encrypted_vault.txt

**encrypted_vault.txt**
>=== BROKEN ENCRYPTION KEY ===
>We recovered this encrypted message from the vault's logs.
Our cryptanalyst noticed something odd about the encryption key...
The modulus seems unusually vulnerable. Something about the primes?
>
>RSA PARAMETERS:
>n = >141022271607414175713364094809444851068643757337278291003331547608786413290198919380050768669755234119277071058831497467991205368937029451780649994005669095870519315498266228688204895807711132337707038182572530341959866488742974118738028260417102827114688274975929765878700317945788015634814829562858751187593
e = 65537
>
>ENCRYPTED MESSAGE:
>c = 107840687649484004543096605944934334365525617750515128276427639162012913073309302080723470031534422769820589720364949972053321305857332436902622751832928437373645237880766784284675346314323607471538195414030294170048351498025855018972310927740135450635684379013474685012932119494504730684976179370381850672917
>
>HINT: When primes are too close, factorization becomes easier.
>HINT: Look into Fermat's factorization method.

we are given the hint that the 2 prime numbers p and q are close to each other. using fermats factorization theorem this makes factoring n very easy. fermats factorization expresses n as a differnce of 2 perfect square numbers: 

  `n = a^2 - b^2 = (a+b)(a-b)`

  here `p = a - b` and `q = a + b`, so `a = (p+q)/2` and `b = (p-q)/2`, so if `p` and `q` are close, `a` is very close to `p` and `q`, and since `p` and `q` are close, and `p*q` is `n`, `sqrt(n)` is close to `p` and `q` both. hence `a` is also close to the `sqrt(n)`. so in order to find `a`, we just initialize `a` with `sqrt(n)` and increment with 1 until we find a value of `a` such that `a*a - n` is a perfect square. when a value of `a` satisfies this condition, we can also find b, p and q. 

after p and q have been found, the rsa is broken and one can just reverse find the value of the decrypted ciphertext. 

**code to find the ciphertext:**

    import math
    
    n = 141022271607414175713364094809444851068643757337278291003331547608786413290198919380050768669755234119277071058831497467991205368937029451780649994005669095870519315498266228688204895807711132337707038182572530341959866488742974118738028260417102827114688274975929765878700317945788015634814829562858751187593
    e = 65537
    c = 107840687649484004543096605944934334365525617750515128276427639162012913073309302080723470031534422769820589720364949972053321305857332436902622751832928437373645237880766784284675346314323607471538195414030294170048351498025855018972310927740135450635684379013474685012932119494504730684976179370381850672917
    
    a = math.isqrt(n)+1
    while True:
        b2 = (a*a)-n
        b = math.isqrt(b2)
        if b*b == b2:
            print(f"found: {a} {b}")
            break
        else:
            a += 1
            print ("not found ${a}")
    
    p = a-b
    q = a+b
    
    phi = (p-1)*(q-1)
    d = pow(e, -1, phi)
    
    m = pow(c, d, n)
    print(m.to_bytes((m.bit_length() + 7) // 8, byteorder='big').decode())


**decrypted output:**

    KEY:0abc5a8609a164318d5cf34ae3ea25606637a89f3c80419b983857d8c0373971
    FLAG:TDHCTF{vault_breach_decrypted}
