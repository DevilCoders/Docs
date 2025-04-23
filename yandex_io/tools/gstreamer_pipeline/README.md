# How to use
```
# без нормализации
./gstreamer_pipeline --filepath boot.wav
aplay -r 48000 -c 2 output.wav

# с нормализацией
./gstreamer_pipeline --filepath boot.wav --norm --true_peak 10 --integrated_loudness 10 --lufs -14
aplay -r 48000 -c 2 output.wav

# с эквалайзером
./gstreamer_pipeline --filepath boot.wav --equal_config config.json
aplay -r 48000 -c 2 output.wav

# писать в кастомный файл
./gstreamer_pipeline --filepath boot.wav --output boot_output.wav
```
