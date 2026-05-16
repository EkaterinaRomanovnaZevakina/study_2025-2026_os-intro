---
# Front matter
title: "Выполнение внешнего курса stepik 'Введение в Linux'. Раздел №3"
subtitle: "Архитектура компьютеров и операционные системы. Раздел: Операционные системы"
author: "Зевакина Екатерина Романовна"

# Generic options
lang: ru-RU
toc-title: "Содержание"

# Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

# Pdf output format
toc: true
toc-depth: 2
lof: true
lot: true
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt

# I18n polyglossia
polyglossia-lang:
  name: russian
  options:
  - spelling=modern
  - babelshorthands=true
polyglossia-otherlangs:
  name: english

# I18n babel
babel-lang: russian
babel-otherlangs: english

# Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:

# Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric

# Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"

# Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float}
  - \floatplacement{figure}{H}
---

# Раздел 3.1

## Задание 1 в 3.1

[рис. @fig-001]

![Задание 1 в 3.1](../images/s3p1.png){#fig-001 width=70%}

**Пояснения:** Чтобы выйти из редактора vim, необходимо нажать комбтнацию ":", затем "q", затем "Еnter". Это прописано в справочнике по редактору.

## Задание 2 в 3.1

**Формулировка задания:** [рис. @fig-002]

![Задание 2 в 3.1 Формулировка задания](../images/s3p2_1.png){#fig-002 width=70%}

**Выполнение задания:** [рис. @fig-003]

![Задание 2 в 3.1 Выполнение задания](../images/s3p2_2.png){#fig-003 width=70%}

**Пояснения:** Чтобы выполнить данное задание, я открыла редактор vim, ввела строку: Strange_  TEXT  is_here. 2=2 YES! и на практике проверяла каждое утверждение.

## Задание 3 в 3.1

**Формулировка задания:** [рис. @fig-004]

![Задание 3 в 3.1 Формулировка задания](../images/s3p3_1.png){#fig-004 width=70%}

**Выполнение задания:** [рис. @fig-005]

![Задание 3 в 3.1 Выполнение задания](../images/s3p3_2.png){#fig-005 width=70%}

**Пояснения:** Чтобы выполнить данное задание, я открыла редактор vim, ввела 6 строк: one two three four five и на практике проверяла каждое утверждение.

## Задание 4 в 3.1

[рис. @fig-006]

![Задание 4 в 3.1](../images/s3p4.png){#fig-006 width=70%}

**Пояснения:** :%s/Windows/Linux находит каждую строку, содержащую «Windows», и заменяет в ней только первое вхождение «Windows» на «Linux»

# Задание 5 в 3.1

**Формулировка задания:** [рис. @fig-007]

![Задание 5 в 3.1 Формулировка задания](../images/s3p5_1.png){#fig-007 width=70%}

**Выполнение задания:** [рис. @fig-008]

![Задание 5 в 3.1 Выполнение задания](../images/s3p5_2.png){#fig-008 width=70%}

**Пояснения:** Чтобы выполнить данное задание, я открыла редактор vim, вошла в режим visial и на практике проверяла каждое утверждение.

# Раздел 3.2

# Задание 1 в 3.2

[рис. @fig-009]

![Задание 1 в 3.2](../images/s3p6.png){#fig-009 width=70%}

**Пояснения:** Каждая оболочка имеет собственную изолированную историю команд, хранящуюся в памяти процесса.

# Задание 2 в 3.2

**Формулировка задания:** [рис. @fig-010]

![Задание 2 в 3.2 Формулировка задания](../images/s3p7_1.png){#fig-010 width=70%}

**Выполнение задания:** [рис. @fig-011]

![Задание 2 в 3.2 Выполнение задания](../images/s3p7_2.png){#fig-011 width=70%}

**Пояснения:** cd /home/bi/- переходим в папку /home/bi/; touch file1.txt - создаем файл file1.txt; cd /home/bi/Desktop/ - переходим в папку /home/bi/Desktop/, но не перемещаем file1.txt в эту папку. За это отвечает комнада mv.

# Задание 3 в 3.2

**Формулировка задания:** [рис. @fig-012]

![Задание 3 в 3.2 Формулировка задания](../images/s3p8_1.png){#fig-012 width=70%}

**Выполнение задания:** [рис. @fig-013]

![Задание 3 в 3.2 Выполнение задания](../images/s3p8_2.png){#fig-013 width=70%}

**Пояснения:** Я следовала правилам, что имя переменной может содержать - цифры, буквы, _  и начинаться с - буквы или _

# Задание 4 в 3.2

**Формулировка задания:** [рис. @fig-014]

![Задание 3 в 3.2 Формулировка задания](../images/s3p9_1.png){#fig-014 width=70%}

**Выполнение задания:** [рис. @fig-015]

![Задание 3 в 3.2 Выполнение задания](../images/s3p9_2.png){#fig-015 width=70%}

**Пояснения:** 
