# Список tld обслуживаемых балансером единого домена

https://st.yandex-team.ru/TRAFFIC-10147

`domains.txt` - основные домены, они резолвятся на ip из [пула](https://racktables.yandex-team.ru/index.php?page=ipvs&vs_id=957) yandex.ru, для них работает ротация ip адресов.
`domains_other.txt` - домены, выпадающие из данной схемы, у них отдельные ip адреса.
