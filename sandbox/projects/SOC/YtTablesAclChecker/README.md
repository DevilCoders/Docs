## Yt tables ACL checker

Find tables which was private and became open to whole company.
Based on everyday dumps from Yt team: [YTADMIN-8092][1]

### Scheme

1. Compare current day dump with yesterdays dump, if table existed yesterday and missing from current day dump - write it to the result
2. Check list of paths missed from yesterday via `yt.wrapper.get` function and write current ACL if can
3. If subject "yandex" is in effective ACL, then write info about table into result
4. Send results from Yt table to Splunk via HEC
5. Create ticket automatically via scheduled savedsearch


[1]: https://st.yandex-team.ru/YTADMIN-8092
