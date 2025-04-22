# Рекомендации для публикации

1. После проведения LSR необходимо загрузить необработанную запись zoom в bucket lsr в папку raw [здесь](https://yc.yandex-team.ru/folders/foo9fohmc6uh3cpg1b52/storage/buckets/lsr?key=Raw%2F).
2. Создать тикет на расшифровку в очереди TAASCRIPT:
   1. Название расшифровки: `Расшифровка LSR (регулярная)`
   2. Тип: обычная расшифровка, не тезисно.
   3. Описание задачи:
```
Подготовить текст по итогам LSR – это часовая встреча по разбору инцидентов, запись зум, супер-NDA.
Расшифровка нужна для клуба LSR clubs.at.yandex-team.ru/lsr.
Есть технические термины.
Нужно разметить спикеров и непонятные места по инструкции:
https://wiki.yandex-team.ru/communication/taas/guidelines/transcript/
```
   4. Сроки указать исходя из расчет неделя на один LSR.
   5. Графу про файлы пока пропустить.
   6. ABC-сервис: dutysearch.
   ---
3. После создания тикета, отредактируйте описание задачи, подставил в файлы для расшифровки ссылку из п.1.
4. После получения расшифровки, начините делать черновик поста, например в wiki.
При необходимости используйте шаблон:
```
Всем привет! Традиционный пост про то, как не надо делать.
КАРТИНКО_МЕМ
Сегодня мы расскажем про LSR-.
===Что произошло===

===Потери===

===Action Items===
* Тикет_номер


<{Расшифровка встречи



}>

<{Запись Zoom
https://s3.mds.yandex.net/lsr/lsr-*mp4
}>

<#<p><table class="wikisnippet_table" width="100%"><tr class="top"><td width="200" style="border-right:1px solid #eaeaea; padding-right:15px;">
<img src='https://jing.yandex-team.ru/files/lensws/thats-it-yes-thats-it.gif' style="height: 200px">
</td><td width="2%"></td><td>
<h1>P.S.</h1><h2>В расшифровке удается распознать не всех.<br/>Коллеги, если вы часто рассказываете о чем-то на LSR<br/>и хотите, чтобы мы вас узнавали,<br/>пожалуйста, напишите нам об этом.</h2>
</td></tr></table></p>
#>

```
5. Видео записи надо обрезать от лишних моментов, используйте ffmpeg:

| Задача                                       | Команда                                                                                                                                         |
|:---------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------|
| Вырезать кусок из видео без рендера          | `ffmpeg -i zoom_0.mp4 -y -threads 4 -ss 00:31:05 -async 1 -c copy lsr_cut.mp4`                                                                  |
| Вырезать кусок из видео с рендером           | `ffmpeg -i zoom_0.mp4 -y -threads 4 -ss 00:30:05 -async 1 lsr_cut.mp4`                                                                          |
| Сделать gif из видео                         | `ffmpeg -i input.mp4 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif`              |
| Сделать gif из фрагмента видео               | `ffmpeg -ss 30 -t 3 -i input.mp4 -vf "fps=10,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif`  |
| Обработать видео фрагмент для заливки в jing | `ffmpeg -i input.mp4 -c:v libx264 -preset slow -crf 18 -c:a aac -b:a 192k -pix_fmt yuv420p out.mp4`                                             |

6. Залейте видео в bucket LSR [тут](https://yc.yandex-team.ru/folders/foo9fohmc6uh3cpg1b52/storage/buckets/lsr).
7. После успешной публикации видео из п.1 можно удалить.