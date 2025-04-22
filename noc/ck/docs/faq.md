# FAQ

## noc-ck-cli валится с ошибкой SSL

Скорее всего требуется установить локальный сертификат [по инструкции](https://wiki.yandex-team.ru/users/alvassin/kak-ustanovit-yandexinternalca-na-mak/).

Пример для macOS нативного Python3 c [python.org](https://www.python.org/downloads/):
```bash
# Запускаем скрипт 'Install Certificates.command'
/Applications/Python\ $(basename $(dirname $(dirname $(which python3))))/Install\ Certificates.command
# Скачиваем сертификаты
curl https://crls.yandex.net/allCAs.pem | tee -a $(python3 -mcertifi)
```

Пример для macOS python3.8 из brew:
```bash
python3.8 -mpip install certifi
mv /usr/local/etc/openssl@1.1/cert.pem /usr/local/etc/openssl@1.1/cert.pem.bak
ln -s /usr/local/lib/python3.8/site-packages/certifi/cacert.pem /usr/local/etc/openssl@1.1/cert.pem
curl https://crls.yandex.net/allCAs.pem | tee -a $(python3.8 -m certifi)
```
Для Ubuntu самый просто способ:
```bash
sudo apt-get install yandex-internal-root-ca
```
Если решения выше не подходят:
https://wiki.yandex-team.ru/security/ssl/sslclientfix/

## noc-ck-cli валится с ошибкой "You have no role allowing this operation"

Нужно сделать вызов `noc-ck-cli auth` и получить токен


## app.checkist.CheckistValidationError

Ошибка несовпадения hash в noc-ck и cfglister. Надо подождать пока пересчитается hash.

Пример:
```
Job of kind "checkist" is failed due to "app.checkist.CheckistValidationError: Current hash for device 'iva3-s68' does not match. Expected 'b57e0697b2b6c05cc3cf6db285dfec3d', got '36484c0a74753a7291063e4f8c5dedbc'"
```

## AttributeError: 'NoneType' object has no attribute 'write'

Ошибка в checklist. Соединение с чем-то закрылось. Кажется, что это связано с RTAPI

Пример:
```
Job of kind "checkist" is failed due to "AttributeError: 'NoneType' object has no attribute 'write'"
```

## comocutor.exceptions.BadCommand: Unrecognized command

Ошибка в comocutor при применении команды на устройстве. Надо проверить генератор.

Пример:
```
Job of kind "checkist" is failed due to "comocutor.exceptions.BadCommand: Unrecognized command"
```

comocutor.exceptions.BadCommand: Wrong parameter

## comocutor.exceptions.BadCommand: Wrong parameter:

Ошибка в comocutor при применении команды на устройстве. Надо проверить генератор.

Пример:
```

"BadCommand<Wrong parameter,   rule 0 permit vpn-instance MEth0/0/0 source 141.8.128.17628>"
```

## comocutor.exceptions.ConnectionException:

Ошибка в comocutor при подключению к устройству. Надо починить ssh на устройстве.

Пример:
```
Job of kind "checkist" is failed due to "comocutor.exceptions.ConnectionException: unable to connect. errors=[TimeoutError(110, "Connect call failed ('5.255.236.57', 22)"), TimeoutError(110, "Connect call failed ('5.255.236.57', 23)")], conn_fabric=[ConnFabric[functools.partial(<class 'comocutor.streamer.SshStream'>, host='red1-s4.yndx.net', ssh_opts={'kex_algs': ['diffie-hellman-group1-sha1', 'diffie-hellman-group-exchange-sha1'], 'encryption_algs': ['aes128-cbc', '3des-cbc']}), None], ConnFabric[functools.partial(<class 'comocutor.streamer.TelnetStream'>, host='red1-s4.yndx.net'), None]]"
```

## comocutor.exceptions.ExpectTimeout:

Ошибка в comocutor - не смогли попасть на устройство. Надо проверить что там с устройством.

Пример:
```
Job of kind "checkist" is failed due to "comocutor.exceptions.ExpectTimeout"
```

## comocutor.exceptions.AuthError

Ошибка в comocutor - не смогли залогиниться. Если это из-за отсутсвия пользователя noc-ck то его надо выкатить, если что-то еще - то дебажить. Устройство должно входить в предикат \[работает ЦК\]

{% cut "Пример:" %}

```
Traceback (most recent call last):
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/exec.py", line 207, in _execute_job_under_lock
    executed = await job_transition.execute()
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/interpreter/job.py", line 51, in execute
    ret = await JobHandle(self.app, self.bundle, self.job).execute()
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/interpreter/job.py", line 196, in execute
    ret = await action_transition.step()
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/interpreter/action.py", line 437, in wrap
    ret = await method(obj, *args, **kwargs)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/interpreter/action.py", line 468, in step
    ret = await self.run()
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/interpreter/state.py", line 153, in _wrap
    ret = await method(obj, *args, **kwargs)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/interpreter/action.py", line 437, in wrap
    ret = await method(obj, *args, **kwargs)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/interpreter/action.py", line 556, in run
    res = await handle.run()
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/interpreter/action.py", line 799, in run
    self.safe_app(self.app), hostname, ctx, **kwargs
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/declarative/checkist.py", line 13, in checkist_config_md5_validate
    await checkist_client.validate(hostname, config_md5)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/checkist.py", line 34, in validate
    await ann_runner.run(cli_opts)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/app/ann_ck.py", line 55, in run
    ann_call_result.ret, max_retries, ann_call_result.out, ann_call_result.err
app.ann_ck.AnnCallError: Last error code 1. Max retries: 2. Last log:

[11:03:42]   ERROR MainProcess - deploy.py:265 - sas1-a3a.yndx.net AuthError(args=(),auxiliary=None) -- 
[11:03:42]   ERROR MainProcess - deploy.py:791 - Could not retrieve config:  -- host='sas1-a3a.yndx.net'
Traceback (most recent call last):
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/modules/annushka/ann.py", line 438, in <module>
    sys.exit(main())
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/modules/annushka/annushka/lib.py", line 333, in wrapper
    return func(*args, **kwargs)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/modules/annushka/ann.py", line 432, in main
    return parser.dispatch(pre_call=_init, add_help_command=True)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/modules/annushka/annushka/argparse.py", line 252, in dispatch
    return ns.func(*values)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/modules/annushka/ann.py", line 115, in show_current
    write_output(arg_out, _gen_items(rt), len(args.query.resolve_ids(rt)))
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/modules/annushka/annushka/output.py", line 83, in write_output
    first_result = next(items_iter)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/modules/annushka/ann.py", line 105, in _gen_items
    use_mesh=False,
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/modules/annushka/annushka/gen.py", line 294, in old_raw
    config = _old_new_get_config_cli(ctx, device)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/modules/annushka/annushka/gen.py", line 504, in _old_new_get_config_cli
    raise exc
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/comocutor/deploy.py", line 95, in make_device_coro
    logger=dev_logger)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/comocutor/deploy.py", line 66, in bind_coro_args
    device_cls=device_cls, streamer_cls=streamer_cls, logger=logger)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/comocutor/yandex.py", line 440, in make_connection
    await host.connect(timeout=DEFAULT_CONNECT_TIMEOUT)
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/comocutor/devices.py", line 683, in connect
    raise e
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/comocutor/devices.py", line 680, in connect
    await self.login()
  File "/usr/share/python3/venvs/noc-ck/lib/python3.7/site-packages/comocutor/devices.py", line 1123, in login
    raise AuthError()
comocutor.exceptions.AuthError
```

{% endcut %}

[Пример Job: 61de8b35641dbd613e427a98](https://noc.yandex-team.ru/jobs?id=61de8b35641dbd613e427a98&page=1)

## comocutor.exceptions.ExecException: The specified ACL does not exist.

Ошибка в применении конфигурации. Надо проверить что применяется и генератор в ann.

Пример:
```
Job of kind "checkist" is failed due to "comocutor.exceptions.ExpectTimeout"
```

[Пример Job: 61de8b35641dbd613e427a8b](https://noc.yandex-team.ru/jobs?id=61de8b35641dbd613e427a8b&page=1)

## BadCommand\<Too many parameters, undo snmp-agent protocol source-interface Vlanif400\>

Ошибка в применении конфигурации. Надо проверить что применяется и генератор в ann.
