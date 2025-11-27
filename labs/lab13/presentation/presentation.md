---
## Front matter
lang: ru-RU
title: Лабораторная работа №13
subtitle: Настройка пакетного фильтра в Linux (firewalld)
author:
  - Максат Хемраев
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 5 ноября 2025

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

Получить навыки работы с брандмауэром **firewalld**  
и научиться управлять сетевыми правилами через  
`firewall-cmd` и `firewall-config`.

# Ход выполнения работы

## Определение зоны по умолчанию

- Проверена зона по умолчанию → **public**
- Просмотрены доступные зоны и список доступных служб

![Список зон и служб](Screenshot_1.png){ width=70% }

## Анализ активных правил зоны

- Выведен список разрешённых сервисов в зоне `public`
- Сравнены команды:
  - `firewall-cmd --list-all`
  - `firewall-cmd --list-all --zone=public`

![Список разрешённых служб](Screenshot_2.png){ width=70% }

## Добавление сервиса VNC (runtime)

- Добавлен сервис **vnc-server** во временную конфигурацию
- Сервис появился в списке разрешённых

![Добавление vnc-server](Screenshot_3.png){ width=70% }

## Добавление сервиса VNC (permanent)

- Повторное добавление, но теперь *permanent*
- Выполнено `firewall-cmd --reload`
- Сервис стал активным и постоянным

![vnc-server permanent](Screenshot_4.png){ width=70% }

## Добавление порта 2022/tcp

- Включён порт **2022/tcp** в постоянную конфигурацию
- Выполнен `firewall-cmd --reload`
- Порт появился в списке активных правил

![Добавление порта 2022/tcp](Screenshot_5.png){ width=70% }

## Включение сервисов в firewall-config

- Запущена графическая утилита `firewall-config`
- Активированы сервисы: **http**, **https**, **ftp**

![GUI firewall-config](Screenshot_6.png){ width=70% }

## Добавление порта 2022/udp через GUI

- На вкладке *Ports* добавлен порт **2022/udp**

![Добавление порта UDP](Screenshot_7.png){ width=70% }

## Применение настроек

- Для применения постоянных настроек выполнено:
  - `firewall-cmd --reload`
- Все изменения вступили в силу

![Синхронизация конфигурации](Screenshot_8.png){ width=70% }

## Добавление сетевых сервисов

- Разрешены следующие сервисы:
  - **telnet** — через командную строку
  - **imap**, **pop3**, **smtp** — через firewall-config

![Проверка конфигурации](Screenshot_9.png){ width=70% }


# Итоги работы

## Вывод

В ходе работы были изучены инструменты **firewalld**,  
включая добавление сервисов и портов в *runtime* и *permanent*  
конфигурацию, а также настройка правил через `firewall-config`.
