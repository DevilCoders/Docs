# Tool to automate requests for ssh/sudo on nanny services

Tool will extract gencfg groups from nanny and create requests in idm for each one.

[OAuth permissions](https://oauth.yandex-team.ru/client/3186a7e063d04c88824e0a904985c381)

Example:
./mass_idm_requests -g basesearch -s jupiter_base -m "automated roles" --ssh --simulate --ssh2token
