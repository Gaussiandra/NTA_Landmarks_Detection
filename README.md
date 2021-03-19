### Описание
[Inclass kaggle контест](https://www.kaggle.com/c/nta-landmarks-detection/overview) по предсказанию координат 194 лицевых точек, где в качестве метрики используется MSE.
##### Пример предсказания написанной модели на тестовых данных
![загруженное (1)](https://user-images.githubusercontent.com/34653515/111840740-f735a400-890d-11eb-97d3-4df9350813c5.png)

##### В лучшем решении использовалась предобученная на лицах [сеть](https://github.com/timesler/facenet-pytorch) с изменённым выходом и большое количество аугментаций на обучении и предсказании.

##### Хороший прирост давали эти подходы:
* Заморзка backbone вначале обучения
* Test Time Augmentation
* Различные аугментации из **albumentations**
* Выкидывание из обучающих данных некорректных примеров с несколькими лицами

##### Подходы, которые не привели к улучшению модели:
* Hard Negatives Mining. Предположение было таким, что сеть будет точнее, если научится корректно работать со сложными примерами.
* Нормализация keypoints
* Детекция лиц и кроп к ним с помощью mtcnn, dlib.
* Добавление координат 68 точек из dlib landmarks detector в fc слои на выходе
* Добавление координат bounding box лица в последние fc
