---
## Front matter
lang: ru-RU
title: Отчёт по лабораторной работе №1
subtitle: Установка Rocky Linux в VirtualBox
author:
  - Максат Хемраев
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 5 сентября 2025

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---


# Цель работы

## Основная цель

Установить и настроить Rocky Linux в VirtualBox, затем проверить работу системы.

# Ход выполнения

## Конфигурация ВМ в VirtualBox

![Конфигурация ВМ (VirtualBox Manager)](image/Screenshot_1.png){ #fig:001 width=70% }

## Выбор языка установки

![Welcome / Language](image/Screenshot_2.png){ #fig:002 width=70% }

## Сводка параметров установки

![Installation Summary](image/Screenshot_3.png){ #fig:003 width=70% }

## Ход установки

![Installation Progress](image/Screenshot_4.png){ #fig:004 width=70% }

## Экран входа (GDM)

![Login screen](image/Screenshot_5.png){ #fig:005 width=70% }

## Установка VirtualBox Guest Additions

![Guest Additions install](image/Screenshot_6.png){ #fig:006 width=70% }

# Проверка системы

## Ядро и CPU (dmesg)

![Kernel & CPU info](image/Screenshot_7.png){ #fig:007 width=70% }

## Гипервизор (dmesg)

![Hypervisor detected](image/Screenshot_8.png){ #fig:008 width=70% }

## Смонтированные файловые системы (mount)

![Mounted filesystems](image/Screenshot_9.png){ #fig:009 width=70% }

# Итоги

## Вывод

Rocky Linux установлен и работает. Выполнена интеграция с VirtualBox (Guest Additions), вход в систему и базовая проверка: ядро, CPU, гипервизор и файловые системы отображаются корректно.
