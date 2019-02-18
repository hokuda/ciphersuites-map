# ciphersuites-map

Print ciphersuites mapping of IANA, OpenSSL, and JSSE in JSON, merging:
* https://www.iana.org/assignments/tls-parameters/tls-parameters-4.csv
* `openssl ciphers -V ALL:COMPLEMENTOFALL`
* `sun.security.ssl.CipherSuite#idMap`

## prerequisite

* install py4j

        $ pip3 install py4j --user

  or

        # pip3 install py4j

## usage

        ciphersuites-map [-h] [-j JAVA]

## optional arguments

        -h, --help            show this help message and exit
        -j JAVA, --java JAVA  path to `java` command
