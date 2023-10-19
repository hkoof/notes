To get the expiry date of an SSL certificate remotely, do:

    echo "" | openssl s_client -connect server:443 >/tmp/cert-info.txt
    openssl x509 -in /tmp/cert-info.txt -noout -enddate
