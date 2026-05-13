---
## Front matter
lang: ru-RU
title: Отчет по выполнению лабораторной работы №1
subtitle: Архитектура компьютеров, раздел Операционные системы
author:
  - Зевакина Екатерина
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 04 мая 2026

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Информация

## Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="70%"}

* Зевакина Екатерина 
* Студентка НКАбд-02-25
* Российсий Универститет Дружбы Народов
* [1032253564@rudn.ru](mailto:1032253564@rudn.ru)

:::
::: {.column width="30%"}

![](image/my_photo.png)

:::
::::::::::::::

## Цель работы

Цель данной работы заключается в изучение основ операционной системы Linux, освоении работы в командной строке, получении навыков администрирования сервера и написания скриптов на языке bush через прохождение внешнего образовательного курса.

## Задание

1. Изучение теорию курса.

2. Выполнить все тестовые задания, подтвердив понимания теории.

3. Выполнить все практические/интерактивные задания в терминале.

4. Написать отчет.

## Теоритическое введение

[Linux (Линукс)](https://www.google.com/search?q=Linux+%28%D0%9B%D0%B8%D0%BD%D1%83%D0%BA%D1%81%29&oq=linux+%D1%8D%D1%82%D0%BE+&gs_lcrp=EgZjaHJvbWUqBwgAEAAYjwIyBwgAEAAYjwIyBwgBEAAYgAQyBwgCEAAYgAQyBwgDEAAYgAQyBwgEEAAYgAQyBwgFEAAYgAQyBwgGEAAYgAQyBwgHEAAYgAQyCAgIEAAYFhgeMggICRAAGBYYHtIBCDc0NjFqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8&ved=2ahUKEwi6_o-ipp2UAxUOFBAIHYDlKUYQgK4QegYIAQgAEAM) — это семейство Unix-подобных операционных систем с открытым исходным кодом, базирующихся на одноименном ядре. В отличие от Windows, Linux бесплатен, чрезвычайно гибко настраивается, безопасен и повсеместно используется на серверах, в суперкомпьютерах, смартфонах (Android) и устройствах интернета вещей. [[1](https://ru.wikipedia.org/wiki/Linux), [2](https://skillbox.ru/media/code/chto-takoe-linux-gayd-po-samoy-svobodnoy-operatsionnoy-sisteme/), [3](https://www.youtube.com/watch?v=CEAzTL1T7-o#:~:text=%D0%9B%D0%B8%D0%BD%D1%83%D0%BA%D1%81%20%E2%80%94%20%D1%8D%D1%82%D0%BE%20%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%86%D0%B8%D0%BE%D0%BD%D0%BD%D0%B0%D1%8F%20%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0%20%D1%81%20%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D1%8B%D0%BC,%D0%B2%201991%20%D0%B3%D0%BE%D0%B4%D1%83%2C%20%D0%BA%D0%BE%D1%82%D0%BE%D1%80%D0%B0%D1%8F%20%D1%81%D1%82%D0%B0%D0%BB%D0%B0%20%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%BE%D0%B9%20%D0%B4%D0%BB%D1%8F), [4](https://handyhost.ru/help/term/chto-takoe-linux.html), [5](https://career.hh.ru/article/vsyo-o-linux-chto-eto-gde-ispolzuetsya-i-s-chego-nachat-izuchenie), [6](https://www.kobzarev.com/linux/why-is-everyone-switching-to-linux/)].

# Выполнение лабороторной работы

# Раздел 1. Введение

