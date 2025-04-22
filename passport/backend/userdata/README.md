## Пайплайн, коротко:
1. yt_steps find_alive_uids
2. `yt read --proxy hahn.yt.yandex.net //tmp/undeleted-uids --format dsv --config "{read_parallel={enable=%true;max_thread_count=50;}}" > undeleted_uids.csv`
3. `cat undeleted_ids.csv | ./bb-dl > data_to_upload`. На выходе возвращаются json для заливки в yt.
4. `cat data_to_upload | yt write --proxy hahn.yt.yandex.net //home/passport/??? --format json`
