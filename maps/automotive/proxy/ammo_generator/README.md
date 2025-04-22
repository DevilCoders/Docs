Run it this way:

```
./ammo_generator \
    --sign-key AAECAwQFBgcICQoLDA0ODw== \
    --user-oauth $(ya vault get version ver-01e8rg76prm3sd2a915cm1xjcq --only-value oauth_token -n) \
    --count 100 \
    > ammo.dat
```
