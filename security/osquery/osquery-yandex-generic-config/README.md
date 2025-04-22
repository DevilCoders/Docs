# OSQUERY General Configuration for Yandex

Adding new tag is very easy just follow these simple steps:
- add it to the postinst in the current directory
- do `dch -i` or increment changelog manually
- add it to the table https://wiki.yandex-team.ru/users/shashial/ycloudosquery/
- add tests to `unt_tests_bash_edition.sh`
- add new tag here https://wiki.yandex-team.ru/users/shashial/ycloudosquerytags/
- rebuild package 
- dmove
- increment number in the instruction https://wiki.yandex-team.ru/users/shashial/ycloudosquerydeploy/