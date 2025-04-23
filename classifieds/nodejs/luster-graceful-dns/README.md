# luster-graceful-dns

Предыстория: [NODULES-438: Сделать конфигурируемым резовинг адреса](https://st.yandex-team.ru/NODULES-438)

## Использование

~~~js
// configs/current/luster.js

module.exports = {
  ···
  extensions: {
    'luster-graceful-dns': {
      family: '/etc/yandex/vertis-nodejs-ip-family.conf'
    }
  }
}
~~~

~~~
› cat /etc/yandex/vertis-nodejs-ip-family.conf

6
~~~
