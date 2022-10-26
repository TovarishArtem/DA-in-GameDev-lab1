# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Чекмарев Артем Алексеевич
- РИ210915

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
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨
## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.
## Задание 1
### Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity.


Установил необходимые пакеты
![Снимок экрана 2022-10-27 013910](https://user-images.githubusercontent.com/114291344/198149108-b475c553-4f76-4742-ba21-ac795e481701.png)


Далее установил приложение "Anaconda", скачал  Torch и соединил с Юнити, потом создал плоскость, шар и куб
После этого добавил скрипт шару и еще добавил Decision Requester и Behavior Parameters:

Скрипт:
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
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
![2022-10-27 01-34-01_Trim](https://user-images.githubusercontent.com/114291344/198150548-74ff9520-2bac-4281-ba00-17b56abdf698.gif)


![Снимок экрана (154)](https://user-images.githubusercontent.com/114291344/198150472-eb71f623-219c-4196-83e0-b963c0da88c2.png)


## Задание 2
### Подробно опишите каждую строку файла конфигурации нейронной сети, доступного в папке с файлами проекта по ссылке. Самостоятельно найдите информацию о компонентах Decision Requester, Behavior Parameters, добавленных сфере.

Decision Requester - запрашивает решение через регулярные промежутки времени.

Behavior Parameters - определяет принятие объектом решений, в него указывается какой тип поведения будет использоваться: уже обученная модель или удалённый процесс обучения.

```yaml
behaviors:
  RollerBall: # Название 
    trainer_type: ppo # Тип обучения с поощрением
    hyperparameters:
      batch_size: 10 # Общее число тренировочных объектов, представленных в одном пакете.
      buffer_size: 100 # Количество опытов, которые необходимо собрать перед обновлением модели.
      learning_rate: 3.0e-4 # Коэффициент скорости обучения — это параметр градиентных алгоритмов обучения нейронных сетей,
                            # позволяющий управлять величиной коррекции весов на каждой итерации. Уменьшается с числом итераций.
      beta: 5.0e-4 # Соответствует силе регуляризации энтропии (мутаций)
      epsilon: 0.2 # Небольшое вещественное число, добавляемое к дисперсии, чтобы избежать деления на 0.
      lambd: 0.99 # Определяет насколько агент полагается на свою текущую оценку стоимости при вычислении обновленной оценки стоимости. 
                  # Низкие значения соответствуют большей зависимости от текущей оценки стоимости,
                  # а высокие значения соответствуют большей зависимости от фактических вознаграждений
      num_epoch: 3 # Число эпох. Эпоха это, когда весь датасет прошел через нейронную сеть в прямом
                   # и обратном направлении только один раз.
      learning_rate_schedule: linear #Определяет как будет меняться скорость обучения, в данном случае - линейно.
    network_settings:
      normalize: false # Соответствует тому, применяется ли нормализация к входным данным векторного наблюдения.
      hidden_units: 128 # Колличество нейронов в одном слое нейронной сети.
      num_layers: 2 # Колличесво слоев нейронной сети.
    reward_signals:
      extrinsic:
        gamma: 0.99 # коэффициент дисконтирования для будущих вознаграждений
        strength: 1.0 # коэффициент, на который умножается необработанное вознаграждение (От 0.01 до 1.0)
    max_steps: 500000 # максимальное число итераций
    time_horizon: 64 # соответствует количеству шагов опыта, которые нужно собрать для каждого агента,
                     # прежде чем добавлять его в буфер опыта. 
    summary_freq: 10000 # через сколько итераций будет промежуточный результат
```    
## Задание 3
### Доработайте сцену и обучите ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны, как и впервом задании, случайно изменять кооринаты на плоскости. 
 Создал еще один куб и передел скрипт
 
 Скрипт:
 ```C#
 using Unity.MLAgents;
using Unity.MLAgents.Actuators;
using Unity.MLAgents.Sensors;
using UnityEngine;

public class RollerAgent : Agent
{
    private Rigidbody rBody;
    [SerializeField] private Transform targetOne;
    [SerializeField] private Transform targetTwo; // Добавил второй обьект-цель
    [SerializeField] private float forceMultiplier = 10;
    private float delta = 1.42f;
    
    private Vector3 GetRandomPosition => new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    private Vector3 GetMiddle(Vector3 v1, Vector3 v2) => (v1 + v2) / 2;
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }
    
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        targetOne.localPosition = GetRandomPosition;
        targetTwo.localPosition = GetRandomPosition; // также задаю ему случайное положение по окончанию эпизода.
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        // нахожу середину и добавляю ее в "чувства" агента
        var middle = GetMiddle(targetOne.localPosition, targetTwo.localPosition); 
        sensor.AddObservation(middle);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
  
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);

        var localPosition = this.transform.localPosition;
        var middle = GetMiddle(targetOne.localPosition, targetTwo.localPosition); 
        float distanceToMiddle = Vector3.Distance(localPosition, middle);
        
        // проверяю достиг ли агент середины.
        if (distanceToMiddle < delta)
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
Результат:

![2022-10-27 03-09-54_Trim](https://user-images.githubusercontent.com/114291344/198152596-1d04c2a7-417f-40ce-9b2a-d88eac783147.gif)




## Выводы
## Что такое игровой баланс?
Игровой баланс — в случае с компьютерными развлечениями, это равновесие некоторых характеристик, механик, персонажей, тактик, команд, правил, и то что связано непосредственно с процессом. Он существует в том или ином виде даже в одиночных играх, но по большей части это относится к многопользовательскому опыту.

Игровой баланс — одна из самых сложных сторон игростроения. Разработчик приводит игру к состоянию баланса, меняя игровые характеристики в ходе бета-тестирования. Но окончательно баланс сетевой игры оттачивается в течение некоторого времени после выхода самой игры, так как это сложный процесс подгонки самых незначительных отклонений от сбалансированного значения.
## Как системы машинного обучения могут быть использованы для того, чтобы игровой балнанс скорректировать?
Главным преимущестовом  нейронных сетей является их гибкость и адаптивность. Благодяря этому они иогут нейросети управлять некоторым аспектом игрового баланса, например экономикой, и дать ей возможность обучаться, ттем самым облегчить работу разработчика. Машинное обучение может мгновенно отреагировать на некоторый триггер
в игровом процессе и сразу же донести информацию до разработчика.

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
