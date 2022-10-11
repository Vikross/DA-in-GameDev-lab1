# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
- Емелькина Виктория Евгеньевна
- РИ210947

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

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
Познакомиться с программами для передачи данных между google, Python и Unity.

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity.
Ход работы:

1. В облачном сервисе google console подключить API для работы с google sheets и google drive.

![1](https://user-images.githubusercontent.com/94571271/195167316-500a800d-63bb-432c-9fa0-1c65c2bbe6f7.jpg)

![2](https://user-images.githubusercontent.com/94571271/195167353-3959de18-8d73-4699-8563-42454c999c44.jpg)


2. Реализовать запись данных из скрипта на python в google-таблицу. Данные описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с учётом стоимости игрового объекта в каждый период.

![3](https://user-images.githubusercontent.com/94571271/195167486-3a5b02a7-2cf9-4fe4-b435-86e934538d18.jpg)

![4](https://user-images.githubusercontent.com/94571271/195167971-1a94a3a2-9b23-4c2c-bece-d6e524c35a4e.jpg)

3. Создать новый проект на Unity, который будет получать данные из google- таблицы, в которую были записаны данные в предыдущем пункте.

![5](https://user-images.githubusercontent.com/94571271/195168307-3f9ee17b-18d5-456e-b155-3ca52e7af2ac.png)


4. Создать новый проект на Unity, который будет получать данные из google- таблицы, в которую были записаны данные в предыдущем пункте.

![c1](https://user-images.githubusercontent.com/94571271/195170909-f7bd971e-4d62-497d-9aa1-e25b295afb35.jpg)

![c2](https://user-images.githubusercontent.com/94571271/195170925-e413b7c1-9191-4a63-99a0-5ebc4c5c5e0a.jpg)

![c3](https://user-images.githubusercontent.com/94571271/195170938-5abac091-8ea9-45d3-9dd1-12201af7698f.jpg)


## Задание 2
###Реализовать запись в Google-таблицу набора данных, полученных с помощью линейной регрессии из лабораторной работы № 1.

Для этого можно взять код из предыдущей работы и немного его изменить(import gspread, изменяем значения в иттерации).

![и1](https://user-images.githubusercontent.com/94571271/195174126-6ca9cad6-5f6f-4b1c-8feb-18d597d0c592.jpg)

![персер](https://user-images.githubusercontent.com/94571271/195177310-0078af35-cd94-4b8c-a1f1-9495831555c2.jpg)

![и3](https://user-images.githubusercontent.com/94571271/195174151-d1b784f5-fd6e-42bc-817c-69171a9139c7.jpg)

Далее принтом выводим значения и видим, что данные в коде и талице одни.

![дан1](https://user-images.githubusercontent.com/94571271/195174910-bae2f0f5-81e4-4cfa-9f77-345eac190e1a.jpg)

![дан2](https://user-images.githubusercontent.com/94571271/195174922-3f8eba5d-70cf-4ef5-b315-d32a5dfbc228.jpg)


## Задание 3
### Самостоятельно разработать сценарий воспроизведения звукового сопровождения в Unity в зависимости от изменения считанных данных в задании 2.


## Выводы

После данной лабораторной работы я научилась работать с Google-таблицами с помошью написания кода на Python, а также получать данные из этих таблиц в Unity.

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
