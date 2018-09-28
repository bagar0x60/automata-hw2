## Запуск скрипта
Для запуска необходим `python 3.7` и пакеты `pillow` и `graphviz`.
Установка пакетов при наличии `pip`:
```bash
# pip install pillow
# pip install graphviz
```
Чтобы рисовать автоматы, надо установить и сам `graphviz`, а не только `python` пакет. На убунту:
```bash
apt-get install graphviz
```
На Windows надо скачать [установщик](https://graphviz.gitlab.io/_pages/Download/Download_windows.html) и после установки добавить путь до `graphviz/bin` в `PATH`.

Описание конечных автоматов хранится в `json` файлах в папках `/1` и `/3`. Чтобы минимизировать автомат, необходимо запустить скрипт `/src/minimizer.py`:
```bash
cd /src
python minimizer.py ../3/example.json
```
В результате работы скрипта в папке с `json` описанием автомата появится `json` описание минимизированного автомата. Для файла `<name>.json` будет сгенерирован файл `<name>_minimized.json`. Так же, в той же папке, будут сгенирированны `png` изображения исходного и минимизированного автоматов с очевидными именами.

На вход скрипту можно передать сразу несколько автоматов, перечисленных через пробел:
```bash
python minimizer.py ../3/test0.json ../3/test1.json ../3/test3.json 
```

В папке `/3` содержатся примеры атоматов для тестирования минимизации. Автомат `/3/example.json` - это автомат из примера к 3 заданию.

## Описание формата хранения автомата
Автомат хранится в формате `json`. Пример:
```json
{
    "alphabet": ["a", "b", "c"],
    "states_count": 2,
    "initial_state": 0,
    "final_states": [0, 1],
    "state_transition_function": [
        [0, "a", 0], [0, "b", 1], [1, "a", 1], [1, "b", 1], [1, "c", 1]
    ]
}
```
Состояния нумеруются целыми числами, начиная с нуля. Поле `"state_transition_function"` задает функцию перехода и содержит тройки вида: `[начальное состояние, символ перехода, итоговое состояние]`. Не все переходы обязаны присутствовать, при необходимости, программа сама добавит стоковую вершину, чтобы сделать автомат полным. Список `"final_states"` может быть пустым.