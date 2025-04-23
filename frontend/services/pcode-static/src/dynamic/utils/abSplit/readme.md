# AbSplit

Скрипт, который делит трафик 50/50 между кодом адфокс и кодом adsense (или любыми другими).

## Использование

```html
<script async src="https://yastatic.net/pcode-dynamic/utils/ab-split.js"></script>

<div id="ad-container"></div>
```

```js

window.absplit = window.absplit || [];
window.absplit.push([
    {
        name: 'Adfox',
        weight: 1,
        script: 'https://yastatic.net/pcode/adfox/loader.js',
        async: false,
        code: function() {
            window.Ya.adfoxCode.create({
                ownerId: 252407,
                containerId: 'ad-container',
                params: {
                    pp: 'i',
                    ps: 'cofz',
                    p2: 'gcnf',
                    puid17: ''
                }
            });
        },
    },
    {
        name: 'NativeRoll',
        weight: 1,
        init: function() {
            (function (a, b, c, d, e, f, g, h) {
                g = b.createElement(c);
                g.src = d;
                g.type = "application/javascript";
                g.async = !0;
                h = b.getElementsByTagName(c)[0];
                h.parentNode.insertBefore(g, h);
                a[f] = [];
                a[e] = function () {
                  a[f].push(Array.prototype.slice.apply(arguments));
                }
            })(window, document, "script", (document.location.protocol === "https:" ? "https:" : "http:") + "//cdn01.nativeroll.tv/js/seedr-player.min.js", "SeedrPlayer", "seedrInit");
        },
        code: function() {
            window.SeedrPlayer({
                container: '#ad-container',
                desiredOffset:50,
                gid: '5679aaaa64225d49248b456b',
            });
        },
    },
    {
        name: 'Google',
        weight: 1,
        script: 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js',
        code: function() {
            var ins = document.createElement('ins');
            ins.className = 'adsbygoogle';
            ins.setAttribute('style', 'display:inline-block;width:240px;height:600px');
            ins.setAttribute('data-ad-client', 'ca-pub-9654582242169983');
            ins.setAttribute('data-ad-slot', '8282588621');

            document.getElementById('ad-container').appendChild(ins);
            (window.adsbygoogle = window.adsbygoogle || []).push({});
        }
    }
]);
```
