# Decode info from Market debug QRs

1. Scan QR-code with iPhone/Android camera
2. Copy base64-looking string from the QR into clipboard. You may sand it to your computer using Telegram
3. Decode information from the QR using this or any other tool

Decoding example:

```console
$ qr-tool ESIQ9LFsHLE9

QR [ESIQ9LFsHLE9] decodes into: uid=1234567890987654321, day=29 (maybe 2021-12-29), is_logged_in=true`
```

Encoding example:

```console
$ qr-tool 1234567890987654321 29 -l

ESIQ9LFsHLE9
```

# Installation instructions:
1. Install Rust: https://www.rust-lang.org/tools/install
1. Restart the console/shell
1. Checkout the tool code: `svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/tools/b2c/qr-tool`
1. Install the tool: `cargo install --path qr-tool`
1. Run the tool:
   * `$ qr-tool 1234567890987654321 29 -l`
   * `$ qr-tool ESIQ9LFsHLE9`
   * `$ qr-tool -h`

# Alternative tools

In case you don't want to deal with Rust you may use following alternative tools for QRs decoding:
* Python: svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/tools/b2c/qr.py
* Web plugin. Contact Alexey Semin for the details

# Finding user's logs
UID + guessed date + time from the screenshot could be used to find user's log:
https://tsum.yandex-team.ru/pipe/https://wiki.yandex-team.ru/users/osialx/kak-najjti-logi-polzovatelja-na-markete/
