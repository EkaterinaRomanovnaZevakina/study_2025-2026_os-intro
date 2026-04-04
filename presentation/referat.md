---
## Front matter
title: "Доклад на тему: Проверка неизменности системных файлов и директорий."
subtitle: "Архитектура компьютеров и операционные системы. Раздел: Операционные системы"
author: "Зевакина Е. Р."

## Generic options
lang: ru-RU\
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt

## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
  - spelling=modern
  - babelshorthands=true
polyglossia-otherlangs:
  name: english

## I18n babel
babel-lang: russian
babel-otherlangs: english

## Fonts
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

## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric

## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"

## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---


# Введение
Тема проверки неизменности системных файлов и директорий (File Integrity Monitoring, FIM) — это фундаментальная часть обеспечения безопасности и администрирования UNIX-подобных систем (Linux, FreeBSD, macOS и др.).

Простыми словами: это процесс, который позволяет ответить на вопрос — «Не изменился ли какой-либо важный системный файл с момента последней проверки?»

Давайте разберем тему системно: зачем, что проверять, как это работает, основные инструменты и что делать с результатами.

# Зачем это нужно?

Системные файлы могут измениться по двум причинам:
1. **Легитимная** (разрешенная администратором):
   - Установка или обновление пакетов (через apt, yum, pkg).
   - Изменение конфигураций (правка sshd_config, fstab, resolv.conf).
   - Самостоятельная компиляция и установка софта.
2. **Нелегитимная** (опасная):
   - Взлом (компрометация) — злоумышленник заменяет ls, ps, sshd или libc.so на свои версии (руткиты).
   - Ошибка администратора (например, chmod 777 /etc/shadow).
   - Сбой ПО или диска — битые сектора, случайное повреждение.
   - Внутренний нарушитель.

**Цель проверки**: обнаружить неавторизованные изменения как можно раньше, особенно на серверах, которые смотрят в интернет.

# Что именно проверять?

Нельзя проверять всё — это займет слишком много времени и ресурсов. Обычно в список входят:
- **Исполняемые файлы:** /bin, /sbin, /usr/bin, /usr/sbin, /usr/local/bin
- **Системные конфигурации:** /etc (почти всё, но особенно passwd, shadow, sudoers, ssh/, pam.d/)
- **Библиотеки:** /lib, /lib64, /usr/lib
- **Ядро и загрузчик:** /boot, модули ядра (/lib/modules)
- **Логи**: чтобы заметить их удаление.
- Ваши собственные скрипты или бинарные файлы.

В UNIX хорошая практика — проверять **все, что не является пользовательскими данными** (домашние папки /home обычно исключают, если это не целенаправленная проверка).

# Как выполняется проверка? (Хэш-суммы и база знаний)

Идея очень простая, но гениальная:
1. Создание эталонной базы («слепка») — в чистом, доверенном состоянии системы.
   - Для каждого проверяемого файла вычисляется криптографическая хэш-сумма (обычно SHA256 или SHA512). Иногда также сохраняются права доступа, владелец, размер, время модификации.
   - Эти данные сохраняются в защищенном месте (локально с правами 0600, на другом сервере, на USB-флешке, в Git).
2. Регулярная проверка — по расписанию (cron, systemd timer).
   - Утилита заново вычисляет хэши всех файлов из списка.
   - Сравнивает их с эталонными.
3. Оповещение — если хэш не совпал (файл изменился), выдается предупреждение: «Файл /bin/ps изменился! Возможно, руткит».

> Почему хэш, а не просто дата изменения?

Дату легко подделать (touch), а хэш уникально соответствует содержимому. Даже 1 байт разницы → хэш полностью меняется.

# Основные инструменты в UNIX
## Классические системные утилиты (ручной способ)

Это базовый уровень, который есть везде.

```
# Создать базу (список хэшей всех файлов в /bin)
find /bin -type f -exec sha256sum {} \; > baseline_bin.txt
# Проверить (сравнить)
sha256sum -c baseline_bin.txt
```

Но у этого способа минусы:
- Не хранит метаданные (права, владельца).
- Нет логики «ожидаемое изменение» (например, после обновления всё сломается).
- Медленно для больших директорий.

## Специализированные инструменты (рекомендуются)
|   Инструмент   |                                                                   Особенности                                                                 |       Где работает     |
|----------------|-----------------------------------------------------------------------------------------------------------------------------------------------|------------------------|
|      AIDE      |       Самый популярный. Свой конфиг, хранит хэши, права, ссылки. Умеет исключать (/etc/.*~). Есть база данных в текстовом виде.    |    Linux, BSD, macOS   |
|    Tripwire    |            Классика (1992). Более сложный, но мощный. Разделяет политику и базу. Платный Open Source версия существует.                    |      Linux, Unix       | 
|    Osquery     |  Современный инструмент от Facebook. Работает через SQL (SELECT * FROM file WHERE path = '/bin'). Позволяет делать очень гибкие проверки.  |  Linux, macOS, Windows |
|    Samhain     |                    Может работать как клиент-сервер, шифровать базу, скрывать процесс. Хорош для HIPAA / PCI DSS.                        |          Unix          |
|    Integrit    |                                  Простой и быстрый, минималистичный.                                                                          |          Unix          |

**Пример с AIDE (классика):**
1. Установка: sudo apt install aide
2. Настройка (/etc/aide/aide.conf):
```
# Определяем правила
FIPSR = p+i+n+u+g+s+m+c+sha256
# Куда смотреть
/bin/   FIPSR
/sbin/  FIPSR
/etc/   FIPSR
!/etc/mtab   # исключить
```

3. Инициализация базы: sudo aideinit
4. Ежедневная проверка: aide --check (есть разница — отправить письмо)
5. После легитимного обновления системы: sudo aide --update

## Проверка через пакетный менеджер (быстрый способ)

Проверяет не по хэшам, а по контрольным суммам из репозитория.

