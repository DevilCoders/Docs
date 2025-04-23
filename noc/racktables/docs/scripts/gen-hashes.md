# Генерируем хеши для локальных учеток

## Назначение
Если предполагается раскатка локального пользователя `userlogin` на девайсы, находящиеся
под управлением localuser-db, то нужно в CVS `noc/switches/autoload/priviges.inc.m4`
закоммитить нужные хеши.
По-умолчанию мы считаем, что это не нужно.

## Процесс генерации
На серверах RT в директории установки есть скрипт `scripts/localuser-db/gen-hashes.php`.
Стоит отметить, что для генерации второго хеша для huawei скрипт ходит одну из железок `{тестовый свитч} and {Huawei CE}`.
```shell
$ scripts/localuser-db/gen-hashes.php -h
Generate all needed hashes for our switches

gen-hashes.php [-h|--help|-v|--verbose] LOGIN

	LOGIN       username

Options:
	-h
	--help		Show this text
	-v
	--verbose	Enable debug logging and send it to stderr
```
Пример использования:
```shell
$ sudo -Hu racktables scripts/localuser-db/gen-hashes.php userlogin
Enter password:
Enter password again:
Huawei hashes: 4`1/E9Z\Va+Q=^Q`MAF4<1!! $1c$GQ871ds1'O$M'+27b0ChVtYd>,3*S:'14jtX-bM!MOX]J0{9hQ$$
M4 define one of:
	HUAWEI_USER(userlogin, 1, !!base64!!NGAxL0U5WlxWYStRPV5RYE1BRjQ8MSEh!!, !!base64!!JDFjJEdRODcxZHMxJ08kTScrMjdiMENoVnRZZD4sMypTOicxNGp0WC1iTSFNT1hdSjB7OWhRJCQ=!!)
	HUAWEI_USER(userlogin, 3, !!base64!!NGAxL0U5WlxWYStRPV5RYE1BRjQ8MSEh!!, !!base64!!JDFjJEdRODcxZHMxJ08kTScrMjdiMENoVnRZZD4sMypTOicxNGp0WC1iTSFNT1hdSjB7OWhRJCQ=!!)
Cisco/Juniper hash: $1$gPsN$Os7HbxS5GUlU1OM9sGXAt/
M4 define one of:
	CISCO_USER(userlogin,5,`$1$gPsN$Os7HbxS5GUlU1OM9sGXAt/')
	CISCO_USER(userlogin,15,`$1$gPsN$Os7HbxS5GUlU1OM9sGXAt/')
Extreme hash: gPsN$Os7HbxS5GUlU1OM9sGXAt/
```
