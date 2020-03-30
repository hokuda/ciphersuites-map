* generic usage

        ciphersuites-map | jq -C . | less -S

* show only iana and openssl name

        ciphersuites-map | jq -C '.[] | {'iana':.iana.name,'openssl': .openssl.name}'

* filter with exact match

        ciphersuites-map | jq -C '.[] | select(.iana.name == "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256") | {'iana':.iana.name,'openssl': .openssl.name}'
