# ciphersuites-map

Print ciphersuites mapping of IANA, OpenSSL, and JSSE in JSON, merging:
* https://www.iana.org/assignments/tls-parameters/tls-parameters-4.csv
* `openssl ciphers -V ALL:COMPLEMENTOFALL`
* `sun.security.ssl.CipherSuite`

## prerequisite

* install py4j (>=0.10.9.7)

        $ pip3 install py4j --user

  or

        # pip3 install py4j

## usage

        ciphersuites-map [-h] [-j JAVA]

## optional arguments

        -h, --help            show this help message and exit
        -j JAVA, --java JAVA  path to `java` command

## supported java vertion

1.8.0, 11, 17, and 21(though py4j 0.10.9.7 doesn't support java 21;).

## example

        $ ./ciphersuites-map --java /usr/lib/jvm/jre-17/bin/java
