export YT_TOKEN='xxx'
export YT_PROXY=banach

${PATH}/docdump column \
    --src //home/videoindex/full/docbase/prevdata/media.raw \
    --key https://www.youtube.com/watch?v=MDM0yAJjlBo \
    --subkey \
    -c data -d TMediaProperties -c antispamdata -d TSrcFactors -c tags -d TTags \
    -t 100

${PATH}/docdump tnode \
    --src //home/videoindex/full/docbase/prevdata/full_index/direct_index \
    --key www.youtube.com/watch?v=MDM0yAJjlBo \
    -r TDirectIndexRecord \
    -t 100

${PATH}/docdump dynamic \
    --src //home/videoindex/vhs/docbase/dynamic/direct_index \
    --key frontend.vh.yandex.ru/player/10444326619482114044 \
    --key-column GroupingUrl \
    -r TDirectIndexRecord \
    -t 100
