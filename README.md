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
### Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity.
Ход работы:

1. Создала новый пустой 3D проект на Unity.

![юнити 1](https://user-images.githubusercontent.com/94571271/198298804-d32f74d2-8f86-4c8d-8084-3379ecdfcc1f.jpg)

2. Добавила ML Agent в Unity.

![юнити 2](https://user-images.githubusercontent.com/94571271/198299485-de30b524-e7d9-448a-8fc2-0fb367734af7.jpg)

3. Создала на сцене плоскость, куб и сферу.

![юнити 3](https://user-images.githubusercontent.com/94571271/198315396-35c71133-3dba-4854-9688-ab6fca2046f1.jpg)

4. Создала простой C# скрипт-файл и подключила его к сфере.

```py

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    // Start is called before the first frame update
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);

        if(distanceToTarget < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }
}

```
5. Добавила скрипт RollerAgent.cs к сфере и также компоненты Decision Requester, Behavior Parameters.

![юнити 4](https://user-images.githubusercontent.com/94571271/198319526-aa3b0b71-19b5-4ed6-9a5e-7038a51e9423.png)

6. В корень проекта добавила файл конфигурации нейронной сети.

![консоль 3](https://user-images.githubusercontent.com/94571271/198319920-7ed1040c-d6ad-45a5-94af-e2c59768d7e9.png)

7. Запустила работу ml-агента.

![консоль 4](https://user-images.githubusercontent.com/94571271/198321991-52c9a89f-d402-452f-8ead-a89c5400957a.jpg)

8. Сделала 3, 9, 27 копий модели «Плоскость-Сфера-Куб», запустила симуляцию сцены и наблюдала за результатом обучения модели.

![3 копии](https://user-images.githubusercontent.com/94571271/198323081-4a2d0109-8ee6-455c-bf18-12093706f669.jpg)

![9 копий](https://user-images.githubusercontent.com/94571271/198323122-5f355354-3895-4cd8-9c63-6aab4cb3a97c.jpg)

![27 копий](https://user-images.githubusercontent.com/94571271/198323142-dfd3c686-dec2-45f8-aad5-2bb8fb418da9.jpg)

#### Вывод: Я сделала вывод о том, что чем больше копий, тем быстрее выполняется обучение. Также я заметила, что показатели Mean Reward и Std of Reward могут временно ухудшиться.

## Задание 2
### Подробно опишите каждую строку файла конфигурации нейронной сети. Самостоятельно найдите информацию о компонентах Decision Requester, Behavior Parameters, добавленных на сфере.

```py

behaviors:
  RollerBall: # id агента
    trainer_type: ppo # режим обучения (Proximal Policy Optimization)
    
    hyperparameters:
      batch_size: 10 # Определяет количество иинформации, собираемой в ходе одного шага в градиентном спуске.
      buffer_size: 100 # Определяет, сколько информации полученных в ходе выполнения действий будет сохранено в буфере перед тем, как на основе этих данных произойдет обучение или изменение модели.
      learning_rate: 3.0e-4 # Параметр задает величину каждого шага обновления градиентного спуска.
      beta: 5.0e-4 # Параметр задает степень регуляризации энтропии, и определяет, какой будет степень случайности в обновленной политике.
      epsilon: 0.2 # Соответствует допустимому порогу расхождения между старой и новой политиками при обновлении с градиентным спуском.
      lambd: 0.99 # Обозначает то, насколько агент полагается на текущую оценку значения при расчете обновленной ооценки значения.
      num_epoch: 3 # Определяет количество проходов через буфер опыта во время градиентного спуска.
      learning_rate_schedule: linear # Графики скорости обучения определяют, по какому графику будет проводиться корректировка скорости обучения путем снижения скорости обучения.
                                     # linear линейно уменьшает скорость
    network_settings: # Параметры нейронной сети
      normalize: false # К входным данным векторного наблюдения не будет применяться нормализация. 
      hidden_units: 128 # Соответствует количеству единиц в каждом полностью подключенном слое нейронной сети. 
      num_layers: 2 # Определяет количество слоев нейронной сети. 
    reward_signals: # Параметры вознаграждений
      extrinsic:
        gamma: 0.99 # Параметр задает степень значимости будущих вознаграждений.
        strength: 1.0 # Коэффициент, на который умножается вознаграждение, предоставляемое средой.
    max_steps: 500000 # Параметр задает количество шагов моделирования (умноженных на частоту кадров), выполняемых в процессе обучения.
    time_horizon: 64 # Параметр соответствует количеству шагов опыта, которые необходимо собрать для каждого агента, прежде чем добавлять его в буфер опыта.
    summary_freq: 10000 # Количество опыта, который необходимо собрать перед созданием и отображением статистики обучения

```
## Задание 3
### Доработайте сцену и обучите ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны, как и в первом задании, случайно изменять координаты на плоскости. 

```py

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    // Start is called before the first frame update
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target;
    public Transform Target2;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
        Target2.localPosition = new Vector3(Random.value * 8 - 4, 0.5f, Random.value * 8 - 4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(Target2.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);
        float distanceToTarget2 = Vector3.Distance(this.transform.localPosition, Target2.localPosition);

        if(distanceToTarget < 1.42f || distanceToTarget2 < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }
}

```
Проверка работы кода.

![итог](https://user-images.githubusercontent.com/94571271/198333660-87e4cd80-ab90-4ed4-9241-336291c3a613.jpg)

## Выводы

В данной лабораторной работе я научилась загружать в Unity дополнительные пакеты и работать с ними, узнала о важности внутриигрового баланса*.
Игровой баланс* - это баланс между сложностью игры и удовольствием от её геймплея. 
Также я на своем опыте убедилась, что для настройки этого баланса может потребоваться много времени и сил.

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
