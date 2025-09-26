---
## Front matter
lang: ru-RU
title: Лабораторная работа №4
subtitle: Работа с программными пакетами
author:
  - Максат Хемраев
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 16 сентября 2025

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

Получить навыки работы с репозиториями и менеджерами пакетов **dnf** и **rpm** в Linux.

# Ход выполнения работы

## Работа с репозиториями

- Изучены файлы конфигурации в **/etc/yum.repos.d**
- Получен список репозиториев: *AppStream*, *BaseOS*, *Extras*
- Выполнен поиск пакетов с ключевым словом *user*

![Список репозиториев](Screenshot_2.png){ #fig:001 width=60% height=60% }

## Установка и удаление пакетов

- Изучен пакет **nmap**  
- `dnf install nmap` — установка основного пакета  
- `dnf install nmap*` — установка всех связанных компонентов  
- Удаление пакетов: `dnf remove nmap`, `dnf remove nmap*`

![Установка пакета nmap](Screenshot_4.png){ #fig:002 width=60% height=60% }

## Группы пакетов

- Получен список доступных групп  
- Изучена группа **RPM Development Tools**  
- Установлена и удалена через `dnf groupinstall` и `dnf groupremove`

![Информация о группе RPM Development Tools](Screenshot_7.png){ #fig:003 width=60% height=60% }

## История операций DNF

- Использована команда `dnf history`  
- Отменено действие с помощью `dnf history undo`

![История DNF](Screenshot_9.png){ #fig:004 width=60% height=60% }

## Работа с rpm: lynx

- Скачан пакет **lynx** и установлен через `rpm -Uhv`  
- Проверено расположение исполняемого файла (**/usr/bin/lynx**)  
- Получена информация о пакете и документации  
- Удаление пакета — `rpm -e lynx`

![Информация о пакете lynx](Screenshot_11.png){ #fig:005 width=60% height=60% }

## Работа с rpm: dnsmasq

- Установлен пакет **dnsmasq**  
- Определены исполняемые, конфигурационные и документационные файлы  
- Изучены установочные скрипты (создание пользователя, регистрация службы)  
- Удаление пакета — `rpm -e dnsmasq`

![Скрипты пакета dnsmasq](Screenshot_17.png){ #fig:006 width=60% height=60% }

# Итоги работы

## Вывод

В ходе лабораторной работы изучены механизмы управления пакетами с помощью **dnf** и **rpm**.  
Полученные знания позволяют администрировать программное обеспечение, управлять зависимостями и обеспечивать безопасность установки пакетов.  
