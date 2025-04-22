для конвертирования ссылок из корня проекта выполнить

grep -R 'help/text.xml' data -l|grep -v "i-translation"|xargs node data2/utils/convert-help/replace-url.js get_help_url
grep -R -l 'help.yandex.ru' ./data3/desktop.blocks|xargs node ./data3/utils/convert-help/replace-help-domain.js


convert-map.json (соответствие старых и новых идентификаторов) скорее всего уже имеет правильный вид, но если нужно его обновить, то это можно сделать открыв https://wiki.yandex-team.ru/users/nashka/tooltips-id-compliance/ и выполнив в консоли браузера

<pre><code>
var result = {};
$('.b-grid-row:not(.b-grid-row_head_yes)').map(function() {
    var cells = $(this).children(),
        newId = $(cells[1]).find('.wiki-p').text();
    $(cells[2]).find('.wiki-p').text().split(', ').forEach(function(oldId) {
        result[Number(oldId)] = newId;
    })
});
JSON.stringify(result);
</code></pre>
