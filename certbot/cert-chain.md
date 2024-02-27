# Adding `DST Root CA X3` to certificate chain

When we are working with old devices or old softwares (like old android versions before version 7), we need to have this CAPATH in our certificate trust chain.  
We can add this to the certificate when using certbot command like below:  
```bash
certbot renew --key-type rsa --cert-name my.domain.com --force-renewal --preferred-chain "DST Root CA X3"
```
NOTICE: The certbot should be in a version where it supports this `--preferred-chain` command argument.
