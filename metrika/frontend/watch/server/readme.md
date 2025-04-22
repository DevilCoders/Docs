# Альфа-версия локальной баннерокрутилки

## Предназначение

Заменить баннерокрутилку на локалхосте, чтобы:

1. Принимать данные от счётчика, отдавать данные на другим частям метрики.


## Установка

Ставим Node.JS.
Linux: из исходников http://nodejs.org/#download
Windows: готовые бинарники http://node-js.prcn.co.cc/ распаковываем в любую папку, прописываем эту папку в %PATH%
FreeBSD: лучше ставить из портов, порт называется то ли node-dev, то ли dev-node, то ли надо гуглить.
[NVM](https://github.com/creationix/nvm)

## Сертификаты

[Статья](https://alexanderzeitler.com/articles/Fixing-Chrome-missing_subjectAltName-selfsigned-cert-openssl/)
Нужно сгенерировать сертификаты с помошью cкриптов в папке .src/cert.
И добавить в доверенные ~/ssl/rootCA.pem

## Запуск

npm start

