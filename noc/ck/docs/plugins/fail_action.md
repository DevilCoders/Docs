# fail - упасть с ошибкой

Шаг позволяет вывести в лог сообщение и затем прекратить выполнение сценария. 

Пример: останавливаем выполнение, если хеш образа не совпал с аргументом

```yaml
      - name: fail if wrong md5
        fail:
          msg: "Wrong md5sum of FW!"
        when: fw_md5.self != job_vars.fw_version_md5sum
```