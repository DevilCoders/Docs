# Bounces / отлупы

## Как работает return-path

Рассылятор отправляет письма примерно так:

    S: 220 yaback ESMTP 
    C: HELO delivery1h
    S: 250 yabacks
    C: MAIL FROM:<sndr.bnc+L/XXXXXXXX@yandex.ru>
    S: 250 2.1.0 <sndr.bnc+L/XXXXXXXX@yandex.ru> ok
    C: RCPT TO:<somebody@somewhere.tld>
    S: 250 2.1.5 <somebody@somewhere.tld> recipient ok
    C: DATA
    S: 354 Enter mail, end with "." on a line by itself
    C: From: <hello@yandex-team.ru>
    To: <somebody@somewhere.tld>
    Subject: My subject
    
    Body.
    .
    S: 250 2.0.0 Ok: queued on yaback as 1434020576-0pJKNm7m-20srieqVgB
    S: 250 Queued mail for delivery
    C: QUIT
    S: 221 2.0.0 Closing connection.


Адрес для отлупов (sndr.bnc+L/XXXXXXXX@yandex.ru) попадает в заголовок Return-Path.

## Адрес для отлупов

В текущей версии рассылятора адрес для отлупов выглядит так:
 
    sndr.bnc+L/VTNRYkVCWUhCV0pZSGhjWmFRWT06Nzg6MA==@yandex.ru
    
где sndr.bnc - это собственно имя ящика, а часть после знака "+" - это закодированная пара "идентификатор рассылки и email получателя"
    
## Как обрабатываются баунсы

Письма с отлупами попадают в ящик sndr.bnc@yandex.ru 

Скрипт из приложения fan_feedback.bounces периодически забирает их по imap, парсит и отписывает.

Логика отписки: если получили 3 permanent failure или 10 temporary failure, то добавляем email в список "глобально отписанных", после чего на этот email перестают отправляться любые рассылки.

