Пример тренировки и вывода сетки для тренировки предсказания на moving MNIST наборе (2 объекта, 10 + 10 фреймов) 
Нужен TensorFlow не ниже 1.4 
Перед запуском надо скачать набор при помощи get_dataset.sh 
Тренировка запускается: 
python ./train.py 
Сделать тестовые картинки c использованием натренированной сети можно (надо внутри выставить индекс эпохи) 
python ./test.py 


Всякие параметры можно крутить в train.py в том числе попробовать два варианта модели (обычный и условный предсказатели)

Пара статей по теме:
Nitish Srivastava, Elman Mansimov, Ruslan Salakhutdinov. "Unsupervised Learning of Video Representations using LSTMs"
Xingjian Shi, Zhourong Chen, Hao Wang, Dit-Yan Yeung. "Convolutional LSTM Network: A Machine Learning Approach for Precipitation Nowcasting"
