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
Ознакомиться с работой перцептрона.

## Задание 1
### В проекте Unity реализовать перцептрон, который умеет производить вычисления.
Ход работы:

1. Добавить пустой объект и подключить к нему скрипт Perceptron.

![image](https://user-images.githubusercontent.com/94571271/205273601-387136ab-8d5e-48ed-ba87-7b33707eaa7a.png)

2. В ходе выполнения работы был добавлен скрипт Perceptron.cs

```py

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(4);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));	
	}
	
	void Update () {
		
	}
}

```
3. В проекте юнити реализовать перцептрон, который умеет выполнять логические операции OR, AND, XOR, NAND.

3.1 Обучение перцептрона на логическую операцию OR.

![image](https://user-images.githubusercontent.com/94571271/205275019-66ca10c9-796a-4b68-98d2-3e25b744b76d.png)

3.2 Обучение перцептрона на логическую операцию AND.

![image](https://user-images.githubusercontent.com/94571271/205275149-29f9129a-5079-4faa-86f7-8ddee497ca9a.png)

3.3 Обучение перцептрона на логическую операцию NAND.

![image](https://user-images.githubusercontent.com/94571271/205275270-b7dfe89d-e60c-4f8e-aa22-6a79828307a9.png)

В случает обучения перцептрона на логическую операцию NAND понадобилось 7 эпох, а не 4 как ранее.

3.4 Обучение перцептрона на логическую операцию XOR.

![image](https://user-images.githubusercontent.com/94571271/205275578-0f2b0fea-2e67-42eb-818b-71a6f6aae29e.png)

В случает обучения перцептрона на логическую операцию XOR - оно было неуспешно. XOR даже спустя 1000 эпох не смог обучиться и некорректно выполнял вычисления т.к. данная операция из-за линейной модели перцептрона не может разделить плоскость одной линией.

## Задание 2
### Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения.
Ход работы:

1. Менять количество эпох и получать разные значения для каждой логической операции, которые нажно переписать в таблицу, после чего создать диаграмму. 

![image](https://user-images.githubusercontent.com/94571271/205277445-762565d2-494c-4054-b04d-2b7b92130a07.png)

Необходимое количество эпох обучения зависит от значений смещения и веса. 

```py

double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

```

Эта часть кода подтвержает мое утверждение, особенно методы DotProductBias и CalcOutput.

## Задание 3
### Построить визуальную модель работы перцептрона на сцене Unity.
Ход работы:

1. Создадать модель для работы фунции OR. Черные кубы - 1, белые - 0.

![image](https://user-images.githubusercontent.com/94571271/205279838-2c18394f-dc0f-45a2-bd7e-7bbd3c94315b.png)

2. Скрипт на изменение цвета при столкновении.

```py

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ChangeColor : MonoBehaviour
{
    private void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.GetComponent<Renderer>().material.color == Color.white && this.gameObject.GetComponent<Renderer>().material.color == Color.white)
        {
            other.gameObject.GetComponent<Renderer>().material.color = Color.white;
            this.gameObject.GetComponent<Renderer>().material.color = Color.white;
        }
        else
        {
            other.gameObject.GetComponent<Renderer>().material.color = Color.black;
            this.gameObject.GetComponent<Renderer>().material.color = Color.black;
        }
    }
}


```
2. Выполнить.

![image](https://user-images.githubusercontent.com/94571271/205280071-6c438586-a579-4f7d-a034-d0404158ed33.png)


## Выводы

В ходе выполнения 4 лабораторной работы, я познакомилась с работой перцептрона. Реализовала перцептрон, который умеет производить вычисления для разных логических операций, построила графики зависимостей и построила визуальную модель работы перцептрона.

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
