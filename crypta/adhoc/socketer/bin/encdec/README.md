## Encrypt / Decrypt

Reads stdin and encrypts it socket way (or decrypts with -d flag).

Encryption/decryption key should be set to `METRIKA_PRIVATE_KEY` env variable.

```
$ export METRIKA_PRIVATE_KEY='---RSA PRIVATE KEY---...'
$ echo '{"a":11}' | ./encdec 
lYmwImwHXwxxaXFYgN4qvRcn3kD6eFW5iOdE0oDaQ3lSnivXXqdMOZeWFGogGVGMet2R1lmsvN1m9/VOtnncx6flqfT90kY0wjF/q29PLi2YNAuE+j9HT/lK89+J/+dky+rqges01DG91inj+n+735NvXDhyGqSE/f0HnokWW0DHUQfNfH6J/aYVka5WNjoC
$ echo lYmwImwHXwxxaXFYgN4qvRcn3kD6eFW5iOdE0oDaQ3lSnivXXqdMOZeWFGogGVGMet2R1lmsvN1m9/VOtnncx6flqfT90kY0wjF/q29PLi2YNAuE+j9HT/lK89+J/+dky+rqges01DG91inj+n+735NvXDhyGqSE/f0HnokWW0DHUQfNfH6J/aYVka5WNjoC | ./encdec -d
{"a":11}
```
