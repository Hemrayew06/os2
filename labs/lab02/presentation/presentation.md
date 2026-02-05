---
## Front matter
lang: ru-RU
title: Лабораторная работа №2
subtitle: Управление пользователями и группами
author:
  - Максат Хемраев
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 9 сентября 2025

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

Получить представление о работе с учётными записями пользователей и группами пользователей в операционной системе типа Linux.

# Ход выполнения работы

## Проверка пользователя и группы wheel

- Вход под пользователем **mhemraev**
- Определение UID, GID и принадлежности к группе **wheel**

![Проверка пользователя mhemraev](Screenshot_1.png){ #fig:001 width=70% }

## Переход к суперпользователю

- Выполнен вход под **root**
- Проверка подтверждает максимальные права

![Переход на root](Screenshot_2.png){ #fig:002 width=70% }

## Настройка sudoers

- Использована команда `visudo`
- В файле разрешено выполнение команд для группы **wheel**

![Редактирование файла sudoers](Screenshot_2.png){ #fig:003 width=70% }

## Создание пользователей alice и bob

- Создан пользователь **alice**, добавлен в группу *wheel*
- Под alice создан пользователь **bob**

![Создание пользователей alice и bob](Screenshot_3.png){ #fig:004 width=70% }

## Настройка login.defs

- **CREATE_HOME=yes** — создание домашней директории
- **USERGROUPS_ENAB=no** — новые пользователи помещаются в группу *users*

![Изменение login.defs](Screenshot_4.png){ #fig:005 width=70% }

## Настройка .bashrc и /etc/skel

- В /etc/skel добавлены папки *Pictures* и *Documents*
- В .bashrc установлен редактор **vim** по умолчанию

![Изменение .bashrc](Screenshot_5.png){ #fig:006 width=70% }

## Создание пользователя carol

- Создана учётная запись **carol**
- Проверены группы и наличие папок в домашнем каталоге

![Создание пользователя carol](Screenshot_6.png){ #fig:007 width=70% }

## Настройка срока действия пароля

- Для carol установлен срок действия пароля — 90 дней
- Минимальный срок — 30 дней, предупреждение за 3 дня

![Настройка срока действия пароля](Screenshot_7.png){ #fig:008 width=70% }

## Работа с группами

- Созданы группы *main* и *third*
- Добавлены пользователи: alice, bob → main; carol → third

![Работа с группами](Screenshot_8.png){ #fig:009 width=70% }

# Итоги работы

## Вывод
В ходе работы изучены основы управления пользователями и группами в Linux:
- Создание учётных записей
- Настройка паролей и сроков их действия
- Работа с конфигурацией sudoers
- Управление группами пользователей
