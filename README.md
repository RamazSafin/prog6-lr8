# Создание автодокументации Sphinx

## Установка модуля

```sh
python -m pip install
```

*Если будут WARNING, вставить в переменную PATH путь до модуля*

## Создание структуры проекта
```sh
mkdir docs && cd docs
```

## Генерация конфигурационных файлов Sphinx
```sh
sphinx-quickstart
```

## Настройка conf.py
В файле docs/conf.py добавим путь к модулю:

```py
import os
import sys
sys.path.insert(0, os.path.abspath('../..'))

project = 'Игра "Угадай число"'
copyright = '2024, Safin Ramaz'
author = 'Safin Ramaz'
release = '0.1'

extensions = [
    'sphinx.ext.autodoc',
]

templates_path = ['_templates']
exclude_patterns = []

html_theme = 'alabaster'
html_static_path = ['_static']

add_module_names = True
```

## Создание `rst` файлов

`../docs/source/`

Создаем файл `main.rst`:

```rst
main.py
=======

.. automodule:: main
    :members:
```

В той же директории изменяем файл `index.rst` (указали `main`):

```rst
Welcome to Игра "Угадай число"'s documentation!
===============================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:
   
   main

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
```

## Билдим сайт с автодокументацией

*из директории `docs`*

```sh
make html
```

## Переходим в папку со сгенерированной документацией и создаем репозиторий

*из директории `docs`*

```sh
cd build/html
git init
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

## В репозитории на https://github.com настраиваем деплой

*Settings --> Pages --> Выбираем ветку `master` для деплоя*
