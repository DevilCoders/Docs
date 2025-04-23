# Tesseract

Actual installation instructions: https://github.com/tesseract-ocr/tesseract/wiki/Compiling

## How to run

```
git clone --recursive git@github.yandex-team.ru:Billing/docker.git
cd ./docker/tesseract
docker build -t tesseract:latest .
```

## How to use

```
tesseract -l rus {IMAGE_FILE_NAME} -
```

## Training tools

Add ```libicu-dev libpango1.0-dev libcairo2-dev``` and ```make training && make training-install```

## Todo

* Move ```tessdata``` out from container
