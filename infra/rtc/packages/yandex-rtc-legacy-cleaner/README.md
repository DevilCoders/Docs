# Legacy packages and files cleaner

Packages scheduled to remove should be listed in "conflicts" section in
`pkg.json`.

Files scheduled to remove should be listed in
`/usr/share/yandex-rtc-legacy-cleaner/remove_files.txt`.  
This is a simple list with file names separated by new lines.

See other details in [HOSTMAN-673](https://st.yandex-team.ru/HOSTMAN-673)

## How to build package manually

    ya package --debian --checkout --not-sign-debian pkg.json
