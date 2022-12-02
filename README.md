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

В случает обучения перцептрона на логическую операцию XOR - оно было неуспешно. Даже спустя 1000 эпох не смог обучиться и некорректно выполняет вычисления т.к. данная операция из-за линейной модели перцептрона не может разделить плоскость одной линией.

## Задание 2
### Построить графики зависимости количества эпох от ошибки обучения. Указать от чего зависит необходимое количество эпох обучения.

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
### 1. Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, привидите пример выполнения кода, который подтверждает ваш ответ.

Да, она должна стремиться к нулю т.к. loss не сильно изменяется при изменении параметра times функции iterate.

```py

a, b = iterate(a, b, x, y, 2)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x, y)
plt.plot(x, prediction)

a, b = iterate(a, b, x, y, 10000)
prediction = model(a, b, x)
loss = loss_function(a, b, x, y)
print(a, b, loss)
plt.scatter(x, y)
plt.plot(x, prediction)

```
### 2. Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.

Основываясь на моих экспериментах с изменением парамерта Lr и кода функции, я сделала вывод о том, что переменная Lr отвечает за линейную регрессию. ее направление. Пока я эксперементировала с переменной Lr, то заметила, что при увеличении параметра Lr угол между прямой и линией координат становиться больше.

## Выводы

Для выполения данного задания я познакомилась с Unity и google.colad, написав там небольшие и несложные тестовые программы, начала знакомство с их инструментами и тем, почему они удобны. Проделала несколько экспериментов для того чтобы понять для чего нужна та или иная переменная и начала лучше разбираться в данных программах. 

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
