## Пример использования

```use hahn;

PRAGMA File('libbloom_email.so', 'yt://hahn/home/crypta/team/zheglov/libbloom_email.so');
PRAGMA File('bloom_filter', 'yt://hahn/home/crypta/team/zheglov/CRYPTA-15719/eu_emails_filter');
PRAGMA Udf('libbloom_email.so');

$is_eu_email = EuEmailsFilter::Load(FilePath('bloom_filter'));

$emails = AsList(
    "sdfsdaf",
    null,
    "aa@aa.aa",
    "some@email.de",
    "neon.nexon@bk.ru"
);

select ListMap($emails, $is_eu_email);```
