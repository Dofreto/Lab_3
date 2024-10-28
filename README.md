# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Гребёнкин Данил Антонович
- ФО-230005
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | ? |
| Задание 2 | # | ? |
| Задание 3 | # | ? |

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
Разработать оптимальный баланс изменения сложности для десяти уровней игры Dragon Picker.

## Задание 1. Начало работы с прототипом
### Ознакомьтесь с презентацией третьей лекции, оцените структуры игры Dragon Picker. Скачайте и ознакомьтесь с прототипом игры Dragon Picker на движке Unity. Запустите игровую сцену, проанализируйте движение дракона:
### - Какие переменные влияют на движение дракона на сцене? Укажите эти переменные.
### - Какие переменные влияют на сложность игры на сцене? Укажите эти переменные.
Ход работы:
- На движение дракона на сцене влияют параметры скорости дракона и случайное значение изменения направления движения дракона
- На сложность игры на сцене влияют параметры: скорость дракона и падения яйца, частота появления яйца и изменения направления движения дракона, количество и размеры щита

## Задание 2. Начало работы с шаблоном google-таблицы для балансировки игры
### Ознакомьтесь с презентацией третьей лекции, оцените структуры шаблона таблицы для балансировки. Отметьте, как может быть использован шаблон таблицы для визуализации изменения уровней сложности в игре Dragon Picker?
Ход работы:
- Шаблон таблицы может быть использован для отслеживания изменений значений баланса

## Задание 3. Задания к работе
## - Задание 1. Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице.
Ход работы:
- Выбор изменяемых параметров: скорость дракона, частота появления яйца, количество щитов
- Написание кода

```Python
import gspread
import numpy as np
gc = gspread.service_account(filename='dragonpickeranalis-75d63a0aadb4.json')
sh = gc.open("DragonPickerAnalis")

def update_indexs():
    for i in range(1, 11):
        sh.sheet1.update_acell("A" + str(i+1), str(i))

def update_dragon_speed(percent: str):
    current_speed = float(sh.sheet1.acell("B2").value)
    for i in range(3, 12):
        current_speed = str(current_speed * float(str(f"1.{percent}")))
        current_speed = current_speed.split(".")
        current_speed = current_speed[0] + "," + current_speed[1]
        sh.sheet1.update_acell("B" + str(i), str(current_speed))
        current_speed = current_speed.split(",")
        current_speed = float(current_speed[0] + "." + current_speed[1])

def update_time_egg_drop(percent: str):
    tail = 100 - int(percent)
    print(tail)
    current_time = float(sh.sheet1.acell("C2").value)
    for i in range(3, 12):
        current_time = str(current_time * float(str(f"0.{tail}")))
        current_time = current_time.split(".")
        current_time = current_time[0] + "," + current_time[1]
        sh.sheet1.update_acell("C" + str(i), str(current_time))
        current_time = current_time.split(",")
        current_time = float(current_time[0] + "." + current_time[1])

def update_shields_count():
    current_count = int(sh.sheet1.acell("E2").value)
    repeat = 1
    for i in range(3, 12):
        sh.sheet1.update_acell("E" + str(i), str(current_count))
        repeat += 1
        if repeat == 3:
            current_count -= 1
            repeat = 0

if __name__ == "__main__":
    update_dragon_speed("20")
    update_time_egg_drop("10")
    update_egg_speed("05")
    update_shields_count()
```
Визуализация данных в таблице:

![Снимок экрана 2024-10-28 192509](https://github.com/user-attachments/assets/3da42319-8697-4702-854c-37ad380d2f58)


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
