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
### Написать программы Hello World на Python и Unity.
Ход работы:

1. Демонстрация сохранения документа google.colab на свой диск
![На диске](https://user-images.githubusercontent.com/94571271/192746496-242db0ad-61bc-4154-a1c2-a1db67ccae7e.png)

2. Запуск программы с выводом "Hello World!" в google.colab.
![HW GC](https://user-images.githubusercontent.com/94571271/192746731-430576f8-feda-427c-99af-8bc3e5146d90.png)

3.Код в VS для вывода на консоль "Hello World!".
![Unity 1 1](https://user-images.githubusercontent.com/94571271/192747162-f02632d8-635e-4e4f-b7de-c387cd5449e0.png)

4. Вывод сообщения "Hello World1" на консоль в Unity.
![Unity 1 2](https://user-images.githubusercontent.com/94571271/192747418-8d6d9412-eecd-4ebb-b956-74c59725d728.png)

## Задание 2
### В разделе "Ход работы" пошагово выполнить каждый пункт с описанием и примером реализации задачи по теме лабораторной работы.

1. Произвела подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.

![1](https://user-images.githubusercontent.com/94571271/192778703-2758de07-8d15-49d0-8cc4-10747b33f976.png)

2. Определила связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.

![2](https://user-images.githubusercontent.com/94571271/192779176-58976a89-8fe7-4caa-91ec-832b3597f95c.png)

3. Начать итерацию.

ШАГ 1. Инициализация и модель итеративной оптимизации.

![1](https://user-images.githubusercontent.com/94571271/192780154-e24365bd-522c-4b6d-8689-92510990499b.png)

ШАГ 2. На второй итерации отображаются значения параметров, значения потерь и эффекты визуализации после итерации.

![2](https://user-images.githubusercontent.com/94571271/192780255-92d175a7-5926-4e71-84ae-d996e235c047.png)

ШАГ 3. Третья итерация показывает значения параметров, значения потерь и визуализацию после итерации.

![3](https://user-images.githubusercontent.com/94571271/192780344-35caa7b2-8d01-42e3-9471-7a096c4d44e5.png)

ШАГ 4. На четвертой итерации отображаются значения параметров, значения потерь и эффекты визуализации.

![4](https://user-images.githubusercontent.com/94571271/192780444-3f6e95fb-652e-41d4-b583-c0a8d8dfbaac.png)

ШАГ 5. Пятая итерация показывает значение параметра, значение потерь и эффект визуализации после итерации.

![5](https://user-images.githubusercontent.com/94571271/192780518-086d3a3e-fbcc-4bee-996e-d8c5e362fc74.png)

ШАГ 6. 10000-я итерация, показывающая значения параметров, потери и визуализацию после итерации.

![6](https://user-images.githubusercontent.com/94571271/192780633-f0697466-18f8-4803-8816-fb83524126c0.png)

## Задание 3
### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

- Перечисленные в этом туториале действия могут быть выполнены запуском на исполнение скрипт-файла, доступного [в репозитории](https://github.com/Den1sovDm1triy/hfss-scripting/blob/main/ScreatingSphereInAEDT.py).
- Для запуска скрипт-файла откройте Ansys Electronics Desktop. Перейдите во вкладку [Automation] - [Run Script] - [Выберите файл с именем ScreatingSphereInAEDT.py из репозитория].

```py

import ScriptEnv
ScriptEnv.Initialize("Ansoft.ElectronicsDesktop")
oDesktop.RestoreWindow()
oProject = oDesktop.NewProject()
oProject.Rename("C:/Users/denisov.dv/Documents/Ansoft/SphereDIffraction.aedt", True)
oProject.InsertDesign("HFSS", "HFSSDesign1", "HFSS Terminal Network", "")
oDesign = oProject.SetActiveDesign("HFSSDesign1")
oEditor = oDesign.SetActiveEditor("3D Modeler")
oEditor.CreateSphere(
	[
		"NAME:SphereParameters",
		"XCenter:="		, "0mm",
		"YCenter:="		, "0mm",
		"ZCenter:="		, "0mm",
		"Radius:="		, "1.0770329614269mm"
	], 
)

```

## Выводы

Абзац умных слов о том, что было сделано и что было узнано.

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
