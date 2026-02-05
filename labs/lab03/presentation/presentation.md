---
## Front matter
lang: ru-RU
title: Лабораторная работа №3
subtitle: Настройка прав доступа
author:
  - Максат Хемраев
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 13 сентября 2025

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

# Цель работы

## Основная цель

Получение навыков настройки базовых, специальных и расширенных прав доступа в Linux.

# Ход выполнения работы

## Управление базовыми разрешениями

- Созданы каталоги */data/main* и */data/third*
- Установлены владельцы групп: **main**, **third**
- Применены права доступа `770`
- Проверена работа под пользователем **bob**

![Создание каталогов и проверка прав](Screenshot_1.png){ #fig:001 width=60% height=60% }

## Проверка пользователя bob

- Вход под **bob**
- Создан файл **emptyfile** в */data/main*
- Попытка доступа к */data/third* — отказ

![Создание файла emptyfile пользователем bob](Screenshot_2.png){ #fig:002 width=60% height=60% }

## Управление специальными разрешениями

- Под alice созданы файлы **alice1**, **alice2**
- Под bob удалены чужие файлы
- Под root установлены SGID и sticky-бит
- Под alice созданы файлы **alice3**, **alice4** с группой *main*
- Попытка удалить файлы bob → *Operation not permitted*

![Sticky-bit и SGID в каталоге main](Screenshot_4.png){ #fig:004 width=60% height=60% }

## Управление расширенными разрешениями (ACL)

- Для каталога */data/main* → доступ группе **third**
- Для каталога */data/third* → доступ группе **main**
- Проверка с *getfacl*
- Созданы файлы **newfile1**, **newfile2**
- Установлены ACL по умолчанию
- Проверка под пользователем **carol**

![Проверка ACL под пользователем carol](Screenshot_8.png){ #fig:008 width=60% height=60% }

# Итоги работы

## Вывод

В ходе работы были изучены:
- Настройка базовых прав доступа
- Применение SGID и sticky-бита
- Использование ACL для управления расширенными правами
- Практика разграничения доступа и защиты данных в Linux
