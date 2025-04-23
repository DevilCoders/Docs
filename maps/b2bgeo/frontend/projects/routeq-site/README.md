# RouteQ site

Testing:
https://l7test.yandex.com/courier/routeq-landing/[your-branch-name]

Site:
https://routeq.com

Temporary staging:  
https://yandex.ru/courier/routeq


### Dev
Run project:
```
npm install
npm run bunker:pull:dev
npm run dev
```
Open in browser http://localhost:3000/

### Bunker
How to add text to jsx:
1. Transform text in typograf https://typograf.yandex-team.ru/ (Use options 'Исходный текст на английском' and 'Кодирование символов в UTF-8')
2. Use `{{br}}` instead of a `<br />`;
4. Add text to bunker node https://bunker.yandex-team.ru/b2b-geo/routeq-site/text?view=raw
5. Save bunker node
6. `npm run bunker:pull:dev`
7. In jsx use `parseText(bunkerJSON.text['page.section.block.element'])`

### Google analytics
In order to gain access to google analytics counter:
- request mail address in routeq.com (`@tuxxon`)
- request access to google account (`@pavelrasputin`)

