# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
- Чекмарев Артем Алексеевич
- РИ210915

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
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity.
Ход работы:
- В облачном сервисе google console подключила API для работы с google sheets и google drive.
- Реализовала запись данных из скрипта на python в google-таблицу. Данные описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с учётом стоимости игрового объекта в каждый период.

Работа в облачном сервисе google console:
![Снимок экрана (132)](https://user-images.githubusercontent.com/114291344/195158365-f83afac0-7cbc-4494-9714-d2b429140836.png)

Реализаация записи данных из скрипта на python в google-таблицу.
![Снимок экрана (133)](https://user-images.githubusercontent.com/114291344/195159956-96d9fd16-bf7e-41c0-90b8-d67da22a446d.png)

![Снимок экрана (134)](https://user-images.githubusercontent.com/114291344/195160116-40ae6a7a-2ad4-4cbe-a168-2651a11d6970.png)

- Создал новый проект на Unity, который будет получать данные из google-таблицы, в которую были записаны данные в предыдущем пункте.

![Снимок экрана (135)](https://user-images.githubusercontent.com/114291344/195161030-49379c2c-d8da-456a-b821-0b4a525e1704.png)

Скрипт:

![Снимок экрана (136)](https://user-images.githubusercontent.com/114291344/195161203-db0c195e-66c5-4e55-aff5-66080a6daf67.png)

- Написал функционал на Unity, в котором будет воспризводиться аудио-файл в зависимости от значения данных из таблицы:

![Снимок экрана (137)](https://user-images.githubusercontent.com/114291344/195161559-50d5ca5e-5e6d-49e9-932c-0a7150042ab6.png)


## Задание 2
### Реализовать запись в Google-таблицу набора данных, полученных с помощью линейной регрессии из лабораторной работы № 1.

![Снимок экрана (139)](https://user-images.githubusercontent.com/114291344/195163609-af79c026-5933-46ad-a4f3-3b5c4eedca51.png)

![Снимок экрана (140)](https://user-images.githubusercontent.com/114291344/195163685-cbb157c6-bac7-44ad-a701-ffd06d96671e.png)

- Программа на питоне

![Снимок экрана (141)](https://user-images.githubusercontent.com/114291344/195169338-37c843a4-5478-4748-b7dd-33b5877a8c2b.png)






## Выводы

В ходе данной лабораторной работы я выяснил как можно подключить Google-таблицу к коду, как записывать в нее значения. Также что эту таблицу можно связать с Unity.

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
