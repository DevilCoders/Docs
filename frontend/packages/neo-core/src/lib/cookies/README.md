### Работа с куками
- На сервере для работы с заголовками используем функции:  
  [server / set](./server/set.ts)  
  [server / get](./server/get.ts)  
  [server / remove](./server/remove.ts)


- В компонентах предпочтительнее использовать хуки  
  [useCookieСontainer](../../hooks/useCookieContainer.ts)  
  [useCookies](../../hooks/useCookies.ts)

- Для установки кук-счетчиков (если необходимо определить, сколько раз показали баннер/попап)  
  [useCookieСounter](../../hooks/useCookieCounter.ts)

**Выбор типа куки**  
Для того, чтобы выставить куку, нужно указать один из трех её типов:
- техническая
- аналитическая / рекламная
- другая

![выбор типа куки](https://s85myt.storage.yandex.net/rjing/U2FsdGVkX18zzutlDz-OrBaIQ7aeVVE7yESXLICGqz6iiyB1jc-fyHO2lPFiEfk4w2EfZMIz2NDOt604sR4xspZfG8nxNcVP-w7LPxT6UVk?ts=0005bcc678a7072b&content_type=image%2fsvg%2bxml&filename=cookieType.svg&disposition=inline&sign=1bbff5c145996c802829ba096892c94fd60b631f1ef99630c5e4923214690370)

**К кому идти, если есть сомнения в выборе типа куки**
Подскажет [Михаил Черняков](https://staff.yandex-team.ru/4ernyakov)

**Время жизни куки**  
Максимальное время жизни куки - год (почти вечность), чтобы не нарушать gdpr

###Если кука новая не забыть добавить её в аркадию
https://wiki.yandex-team.ru/users/4ernyakov/upravljator-kukami/

https://gdpr.eu/cookies/
