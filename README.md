# Reproduce Bug on MAC

## Generate self signed certs

```bash
cd certs
sh init.sh
cd ..
```

### Works with Node JS v16.18.1

```bash
nvm install 16.18.1
node app.js
# Server starts successfully ...
```

### Failing with Node JS v 17.0.0

The app doesn't start with versions 17.0.0 and afterwards

```bash
nvm install 17.0.0
node app.js
# Server fails with error:
# node:internal/tls/secure-context:65
#     context.setCert(cert);
#             ^

# Error: error:0A00018E:SSL routines::ca md too weak
#     at node:internal/tls/secure-context:65:13
#     at Array.forEach (<anonymous>)
```

### Testing with curl

```bash
cd certs
# Access the site using the client certificate created above.
curl -v -s -k --key snort-key.pem --cert snort-crt.pem https://localhost:4433
```
