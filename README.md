# SuperResolution

Для решения задачи single image super resolution были использованы GAN-ы, а именно SRGAN. 

## Об SRGAN

[Оригинальная статья](https://arxiv.org/pdf/1609.04802.pdf)

SRGAN представляет собой генеративно-состязательную нейросеть для задачи получения фотореалистичных изображений высокого качества из изображений с плохим качеством. 

Генеративно-состязательные сети - это алгоритм, построенный на комбинации из двух нейронных, одна из которых (генератор) генерирует образцы, а другая (дискриминатор) старается отличить правильные («подлинные») образцы от неправильных.

Архитектура генератора и дискриминатора:

![SRGAN structure](images/srgan_architecture.png)

Успех SRGAN в задаче super resolution обусловлен следующими особенностями:

- Генеративно состязательные сети позволяют создавать более реалистичные изображения, чем нейросети, основанные на оптимизации MSE между пикселями. Модели, ориентированные на оптимизацию MSE по пикселям, "усредняли" текстуры, что делало их чрезмерно гладкими.  Использование GAN-ов, благодаря дискриминатору, который учится отличать фейковые сгенерированные изображения от настоящих, позволяет генерировать изображение из множества фотореалистичных вариантов, не усредняя все текстуры. ![Alt Распределение возможных фотореалистичных изображений](images/natural_manifold.png)
- Второй важной особенностью стало использование **Perceptual loss**.  В процессе обучения нейронной сети, оптимизацию по MSE между пикселями заменили на perceptual loss, который представляет из себя MSE, посчитанный в пространстве фичей глубокой сверточной сети (в частности, VGG19). Такая ошибка более инвариантна к изменению пикселей изображения, что предоставляет генератору большую свободу в изменении изображения.