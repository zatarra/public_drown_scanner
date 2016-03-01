DROWN Scanner
=============

This python utility scans for vulnerability to the DROWN attack against TLS.
It is distributed under the GPLv2 license, and includes a specific version of
https://github.com/tintinweb/scapy-ssl_tls (which is also distributed under GPLv2)
and
https://github.com/hiviah/pyx509.
We are grateful to both authors for providing these useful libraries.

This utility was written in an ad-hoc manner in order to identify
only the most common vulnerable configurations.
We emphasize that it cannot accurately detect all vulnerable servers,
and no one should rely on it to confidently determine a particular server is not vulnerable.

In particular, the utility only detects SSLv2 support *by a single port*.
DROWN is made worse by its cross-protocol nature, i.e.
an HTTPS server that doesn't support SSLv2 may be vulnerable
because it shares its public key with an SMTP server that does.
This utility *cannot detect this scenario*, and we strongly recommend
testing servers using our online scanner, at https://drownattack.com.

Likewise, it may also have false positives,
i.e. it may indicate a server is vulnerable when it is in fact not.

Hubert Kario has also made different scanning scripts available here:
https://mta.openssl.org/pipermail/openssl-dev/2016-March/005602.html

Dependencies:
--------------
You need the Python `enum`, `scapy`, and `pycrypto` packages.

On a Debian system: `sudo apt-get install python-enum scapy python-crypto`

Or with pip: `sudo pip install enum pycrypto scapy pyasn1`

Usage examples:
---------------
```
python scanner.py localhost 443
...
python scanner.py localhost 587 -esmtp
...
python scanner.py localhost 143 -imap
...
python scanner.py localhost 25 -esmtp
...
python scanner.py localhost 110 -pop3
...
python scanner.py localhost 443 -bare
````
