* generic usage

        ciphersuites-map | jq -C . | less -S

* show only iana and openssl name

        ciphersuites-map | jq -C '.[] | {'iana':.iana.name,'openssl': .openssl.name}'

* filter with exact match

        ciphersuites-map | jq -C '.[] | select(.iana.name == "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256") | {'iana':.iana.name,'openssl': .openssl.name}'

* script to map cipherscan output

      #!/bin/bash
      
      MAP=$(mktemp)
      SCAN=$(mktemp)
      
      HOST=$1
      PORT=${2:-443}
      
      cipherscan ${HOST}:${PORT} | tee $SCAN
      ciphersuites-map > $MAP
      
      OPENSSL_NAMES=`awk '/prio/,/^$/' < $SCAN | grep '[0-9].*' | awk '{print $2}'`
      
      echo
      
      for name in $OPENSSL_NAMES
      do
          cat $MAP | jq -r -C ".[]
                            | select(.openssl.name == \"${name}\")
                            | [.iana.name, .openssl.name]
                            | @csv"
      done | sed s/\"//g | column -s ',' -t | cat -n

* regex

      ciphersuites-map | jq -C '.[] | select(.iana.name != null) | select(.iana.name | test("(TLS_.*DHE_RSA_WITH_AES_.*_GCM_SHA.*)")) | .openssl.name'
