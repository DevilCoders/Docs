Feel free to contribute. Follow the steps
1. Checkout ```svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/sre/nanny``` or use [Arcanum](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/nanny/front/)
2. Make a change
3. Create ReviewBoard request ```svn ci -m 'review:new'```
4. Publish it
5. Wait for "Ship it!" or "+1" or "LGTM"
6. Commit ```svn ci -m 'review:<id>'```
7. Use [TSUM](http://tsum.yandex-team.ru/pipe/projects) to release configs
You can skip the steps 3-6 and just commit changes but it is not a recommended way.