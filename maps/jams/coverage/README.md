# Jams Coverage Dataset

The dataset can be built with the "ya make" command wich outputs dataset files into the dataset/ directory.
The output includes:
- trf.mms.1;
- coverage.xml;
- coverage.js;

The consistency check of the resulting .mms file may be performed using utils/trf_checker utility:
utils/trf_checker -- -g <path to geoid.mms> -t dataset/trf.mms.1

Production dataset is assembled by the sandbox task:
https://sandbox.yandex-team.ru/task/621426325/view
