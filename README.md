# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Емелькина Виктория Евгеньевна
- РИ210947

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1
### Измените параметры файла, yaml-агента и определите какие параметры и как влияю на обучение модели.
Ход работы:

1. Открыть скачанный проект Unity, ознакомиться с его работой.

![image](https://user-images.githubusercontent.com/94571271/205281789-bc9f6595-9a03-40f9-9e0c-0344607ff778.png)

2. Переместить файл Economic.yaml в папку с проектом Unity.

3. Запустить Anaconda Prompt (от имени администратора). Создать виртуальное пространство.

![image](https://user-images.githubusercontent.com/94571271/205282222-cafb4b3e-e8a5-4f02-9d3c-1971a417fe82.png)

4. Запустить сцену в Unity. Шарик начинает движение от одного кубика к другому. Для того чтобы ускорить процесс обучения – увеличьте количество префабов TargetAreaEconomiс.

5. Устанавить библиотеку TensorBoard (pip install tensorflow) для того, чтобы построить графики оценки результатов обучения. 
Первоначальные данные:

![image](https://user-images.githubusercontent.com/94571271/205282851-22618f07-33cf-4659-8e53-d049e851636b.png)

![image](https://user-images.githubusercontent.com/94571271/205282966-02174957-3ff5-4278-99b8-4587c4142350.png)

![image](https://user-images.githubusercontent.com/94571271/205283048-ad915ca3-4a08-420b-8b29-044668456fd2.png)

6. Изменить параметры yaml-агента.

6.1 Изменить batch_size на 4096.

![image](https://user-images.githubusercontent.com/94571271/205283918-84d69f95-436f-440e-ab98-94be7c027427.png)

![image](https://user-images.githubusercontent.com/94571271/205283969-4bf095cf-6549-475c-a33f-49b174f51815.png)

6.2 Изменить lambd на 0.1.

![image](https://user-images.githubusercontent.com/94571271/205284098-8c01f91e-68cc-4231-bbcd-2c13775bb88c.png)

![image](https://user-images.githubusercontent.com/94571271/205284130-e5e9d048-33d1-43a6-82f5-7d677b900b60.png)

6.3 Изменить buffer_size на 150.

![image](https://user-images.githubusercontent.com/94571271/205284241-764a83b4-6f1b-47d2-8878-f10a63ec24a5.png)

![image](https://user-images.githubusercontent.com/94571271/205284269-b1bc9239-d7c2-4b2f-9663-5efc569363c8.png)

6.4 Изменить num_layers на 100.

![image](https://user-images.githubusercontent.com/94571271/205284421-7567a03b-a583-4022-af7d-9f7a0eab1abd.png)

![image](https://user-images.githubusercontent.com/94571271/205284463-fc1e918a-d109-4a04-b25b-037934df0476.png)

6.5 Изменить epsilon на 1.2.

![image](https://user-images.githubusercontent.com/94571271/205285024-a79aa136-49a6-43a3-bf51-4fdac32167ef.png)

![image](https://user-images.githubusercontent.com/94571271/205285063-72a7f399-7b96-4679-a593-465229cbe5c7.png)

## Задание 2
###Опишите результаты, выведенные в TensorBoard.

1. График Cumulative Reward: должен возрастать, также он не должен превышать 1 по вертикали.

2 .График Episode Length: соответствует количеству решений принятых агентом в течение одного эпизода, должен возрастать.

3. График Policy Loss: средняя величина функции потерь, этот график должен уменьшаться во время успешной тренировки.

4. График Value Loss: Средняя потеря функции обновления значения, этот график должен увеличиваться, пока агент учится, а затем уменьшаться.

Работая с графиками легче понять какие параметры надо менять, а какие - нет.

## Выводы

Работая над этой лабораторной работой я научилась интегрировать экономическую систему в Unity и обучила ей пользоваться Ml Agent. Также я меняла параметры yaml-файла и наблюдала за тем, каким образом это влияет на результаты обучения MLAgent.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
