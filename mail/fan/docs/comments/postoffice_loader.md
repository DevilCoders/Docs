https://tech.yandex.ru/postoffice/doc/dg/reference/stat-view-docpage/


```
curl -i "https://postoffice.yandex.ru/api/1.0/stat-view?oauth_token=***&listid=emm86-17.yandex.ru&domain=yandex-team.ru"
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 26 Apr 2015 21:40:15 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Vary: Accept-Encoding
Cache-Control: max-age=0, must-revalidate, proxy-revalidate, no-cache, no-store, private
Expires: Thu, 01 Jan 1970 00:00:01 GMT
X-Frame-Options: Deny
Strict-Transport-Security: max-age=315360000

{"session":"FpetAgdX",
"subject":"",
"total":9692,
"spam":{"total":91,"instant":0,"read":11,"not_read":80,"not_deleted":91,"personal":0},
"deleted":{"total":3443,"read":732,"not_read":2711,"not_spam":3438},
"read":{"total":1821,"inbox":1079,"spam":10,"deleted":732},
"not_read":{"total":7871,"inbox":5084,"spam":76,"deleted":2711},
"previous":{"total":0,"read":0,"not_read":0,"spam":0,"deleted":0},
"scrolling":[7,19,65,29,49,44,28,32,59,219],
"read_time":[{"sec":10,"count":857},{"sec":20,"count":195},{"sec":30,"count":106},{"sec":40,"count":68},{"sec":50,"count":68},{"sec":60,"count":57},{"sec":120,"count":16},{"sec":180,"count":36},{"sec":240,"count":718},{"sec":300,"count":2},{"sec":360,"count":2},{"sec":420,"count":3},{"sec":480,"count":7},{"sec":540,"count":2},{"sec":600,"count":2},{"sec":660,"count":3},{"sec":780,"count":3},{"sec":840,"count":2},{"sec":1020,"count":1},{"sec":1080,"count":2},{"sec":1320,"count":1},{"sec":1620,"count":2},{"sec":1680,"count":1},{"sec":1740,"count":2},{"sec":1800,"count":1},{"sec":1920,"count":2},{"sec":2280,"count":1},{"sec":2700,"count":2},{"sec":3000,"count":1},{"sec":3300,"count":2},{"sec":3480,"count":1},{"sec":3540,"count":1},{"sec":3600,"count":1},{"sec":7200,"count":4},{"sec":10800,"count":2},{"sec":14400,"count":1},{"sec":18000,"count":1},{"sec":36000,"count":1},{"sec":75600,"count":1},{"sec":86400,"count":1}],
"till_read_time":[{"hour":1,"count":857},{"hour":2,"count":195},{"hour":3,"count":106},{"hour":4,"count":68},{"hour":5,"count":68},{"hour":6,"count":57},{"hour":7,"count":48},{"hour":8,"count":28},{"hour":9,"count":12},{"hour":10,"count":7},{"hour":11,"count":5},{"hour":12,"count":16},{"hour":14,"count":1},{"hour":15,"count":11},{"hour":16,"count":13},{"hour":17,"count":22},{"hour":18,"count":36},{"hour":19,"count":20},{"hour":20,"count":29},{"hour":21,"count":19},{"hour":22,"count":24},{"hour":23,"count":15},{"hour":24,"count":718}],
"read_hour":[{"hour":0,"count":47,"spam":1,"deleted":29},{"hour":1,"count":10,"spam":1,"deleted":3},{"hour":2,"count":14,"spam":0,"deleted":3},{"hour":3,"count":8,"spam":0,"deleted":2},{"hour":4,"count":2,"spam":0,"deleted":1},{"hour":5,"count":8,"spam":0,"deleted":4},{"hour":6,"count":12,"spam":0,"deleted":5},{"hour":7,"count":19,"spam":0,"deleted":10},{"hour":8,"count":41,"spam":0,"deleted":20},{"hour":9,"count":49,"spam":0,"deleted":16},{"hour":10,"count":66,"spam":0,"deleted":24},{"hour":11,"count":80,"spam":0,"deleted":37},{"hour":12,"count":63,"spam":0,"deleted":15},{"hour":13,"count":50,"spam":0,"deleted":16},{"hour":14,"count":182,"spam":0,"deleted":42},{"hour":15,"count":276,"spam":3,"deleted":98},{"hour":16,"count":182,"spam":3,"deleted":72},{"hour":17,"count":144,"spam":0,"deleted":48},{"hour":18,"count":119,"spam":2,"deleted":47},{"hour":19,"count":102,"spam":0,"deleted":46},{"hour":20,"count":97,"spam":0,"deleted":38},{"hour":21,"count":103,"spam":0,"deleted":49},{"hour":22,"count":92,"spam":0,"deleted":32},{"hour":23,"count":75,"spam":1,"deleted":28}],
"cr":{"total":589,"male":515217,"female":482737,"age":[39352,172271,347489,246574,0],"tns":[86067,416160,495631],"int":[403,38,235,357,343,331,365,210,263,407,186,149],"int_affinity_total":327441802,"int_affinity":[263093182,36287812,144293973,245180463,199296813,239505994,231332901,129462716,160283319,256211716,110799327,76166690]},
"dkim":{"pass":9692,"fail":0,"neutral":0}}
```

```
[u'fan-59', u'ikorzyn@yandex-team.ru'] ,
[u'fan-101', u'hello@yandex.ru'] ,
[u'emm91', u'survey@market.yandex.ru'] ,
[u'fan-89', u'hello@yandex.ru'] ,
[u'trash', u'disk-news@yandex-team.com.ua'] ,
[u'emm90_a', u'hello@yandex.ru'] ,  [u'fan-102', u'hello@yandex.ru'] ,  [u'trash', u'disk-news@yandex-team.ru'] ,  [u'maps_8april', u'maps-news@yandex-team.ru'] ,  [u'trash', u'disk-news@yandex-team.com'] ,  [u'mail_for_iphone', u'hello@yandex-team.com'] ,  [u'mail_for_iphone', u'hello@yandex-team.com.tr'] ,  [u'mail_for_iphone', u'hello@yandex-team.com.ua'] ,  [u'android2', u'hello@yandex-team.ru'] ,  [u'EMM-85', u'captcha@support.yandex.ru'] ,  [u'android2', u'hello@yandex-team.com.tr'] ,  [u'trash', u'disk-news@yandex-team.com.tr'] ,  [u'fan-21', u'hello@yandex-team.com.ua'] ,  [u'fan-95', u'hello@yandex.ru'] ,  [u'Debts for lights', u'inform@money.yandex.ru'] ,  [u'mail_for_iphone', u'hello@yandex-team.ru'] ,  [u'emm86-2', u'hello@yandex-team.ru'] ,  [u'emm86-16', u'hello@yandex-team.ru'] ,  [u'emm86-4', u'hello@yandex-team.ru'] ,  [u'emm86-5', u'hello@yandex-team.ru'] ,  [u'emm91', u'survey@market.yandex.ru'] ,  [u'emm86-7', u'hello@yandex-team.ru'] ,  [u'emm86-9', u'hello@yandex-team.ru'] ,  [u'emm90_i', u'hello@yandex-team.ru'] ,  [u'emm86-1', u'hello@yandex-team.ru'] ,  [u'emm86-3', u'hello@yandex-team.ru'] ,  [u'emm86-8', u'hello@yandex-team.ru'] ,  [u'emm86-10', u'hello@yandex-team.ru'] ,  [u'emm86-11', u'hello@yandex-team.ru'] ,  [u'emm86-12', u'hello@yandex-team.ru'] ,  [u'emm86-13', u'hello@yandex-team.ru'] ,  [u'emm86-14', u'hello@yandex-team.ru'] ,  [u'emm86-15', u'hello@yandex-team.ru'] ,  [u'emm86-17', u'hello@yandex-team.ru'] ,  [u'emm86-18', u'hello@yandex-team.ru'] ,  [u'emm86-6', u'hello@yandex-team.ru'] ,  [u'fan-100', u'hello@yandex.ru'] ,
```