# Marty adder

## Description
- Add marty to tg chats
- Usage: `$ marty-adder `
  (For some chats require a `chats_for_append` file. Download file or mount and run marty-adder from arcadia/search/mon/marty-adder)

## Installation
### From pypi.yandex-team
- Install: `pip install -i https://pypi.yandex-team.ru/simple/ marty-adder`
- Upgrade: `pip install --upgrade -i https://pypi.yandex-team.ru/simple/ marty-adder`

### From arcadia
- mount arcadia
- in arcadia/search/mon/marty-adder run: 
`make`


## How-to release to yandex pypi
1. [Get username and password here](https://pypi.yandex-team.ru/accounts/access-keys/)
2. Edit `~/.pypirc` with your username and password
   ```
   [distutils]
   index-servers = yandex
   [yandex]
   repository: https://pypi.yandex-team.ru/simple/
   username: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
   password: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
   ```
3. Build and upload with `python setup.py sdist upload -r yandex`

## NEW! How add additional chats
1. Add invite link in file with name "chats_for_append". (Chat name is not necessary) (Example: "https://t.me/+lnfeuijfnaw Name")  
2. Restart script
