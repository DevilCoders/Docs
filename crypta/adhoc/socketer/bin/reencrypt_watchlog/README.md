## Reencrypt socket data in bs-watch-log.json

Reads input file (defaults to stdin) assuming data to be bs-watch-log in json format.

Looks for the socket data (di key) in browserinfo, tries to decrypt on `$METRIKA_PRIVATE_KEY` and encrypt back on `$METRIKA_TEST_KEY`. Result would be printed to stdout.

Environment variables `METRIKA_PRIVATE_KEY` and `METRIKA_TEST_KEY` must be set accordingly.

If either decryption or encryption fails or there is no socket data - string returns unchanged but errors would be printed to stderr.

```
$ export METRIKA_PRIVATE_KEY='---RSA PRIVATE KEY---...'
$ # public key is sufficient to encrypt but private would do
$ export METRIKA_TEST_KEY='---RSA PUBLIC KEY---...'
$ ./reencrypt_watchlog -i bs-watch-log.json
...

```
