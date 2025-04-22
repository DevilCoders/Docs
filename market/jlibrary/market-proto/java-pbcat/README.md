## Java-pbcat - тулза для чтения протобуфных файлов, написанная на языке java.

Была сделана по аналогии с [pbsncat](https://wiki.yandex-team.ru/market/development/pbufsn/#pbsncat)
[Страничка java-pbcat на вики](https://wiki.yandex-team.ru/market/mbo/descriptiondumpfiles/java-pbcat/)

### Как пользоваться

```shell
usage: java-pbcat [-I <INPUT_FILE>] [-O <OUTPUT_FILE>] [-o
<OUTPUT_FORMAT>] [-c <COMPRESSOR_TYPE>] [-d <DELIMER_TYPE>] [-m
<MAGIC>] [--offset <OFFSET>] [--size <SIZE>] [--total-size] [-v]
[--help] [--version]
-I,--input-file <INPUT_FILE>         Path to input file
-O,--output-file <OUTPUT_FILE>       Path to output file (console by
default)
-o,--output-format <OUTPUT_FORMAT>   Output format: <text|json|xml> (text
by default)
-c,--compressor <COMPRESSOR_TYPE>    Compressor: <auto|none|gzip|snap>
(auto by default)
-d,--delimer <DELIMER_TYPE>          Delimer type: <none|varint|le>
(varint by default)
-m,--magic <MAGIC>                   Magic 4 letter string (Ex. --magic
MSML). If param is set, will ignore
magic from input file
--offset <OFFSET>                 Offset to start with (Ex. --offset
10)
--size <SIZE>                     Size of printed messages (Ex. --size
5)
--total-size                      Prints only total size of messages
-v,--verbose                         Print debug information to console
--help                            Print help information
--version                         Print java-pbcat and market-proto
versions
```

### Как установить

* устанавливаем `arc`, если еще не установлен. Гайд [тут](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)
* выполняем в терминале команды:
```shell
ya make $HOME/arcadia/market/jlibrary/market-proto/java-pbcat/
chmod 755 $HOME/arcadia/market/jlibrary/market-proto/java-pbcat/java-pbcat.sh
## Можно выполнить только одну из команд внизу
## чтобы тулза вызывалась либо по команде 'java-pbcat', либо просто 'pbcat'
echo "alias java-pbcat='$HOME/arcadia/market/jlibrary/market-proto/java-pbcat/java-pbcat.sh'" >> ~/.bashrc && source ~/.bashrc
echo "alias pbcat='$HOME/arcadia/market/jlibrary/market-proto/java-pbcat/java-pbcat.sh'" >> ~/.bashrc && source ~/.bashrc
```
* перезагружаем терминал и можно пользоваться
