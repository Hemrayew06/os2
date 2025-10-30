---
## Front matter
lang: ru-RU
title: Лабораторная работа №9
subtitle: Управление SELinux
author:
  - Максат Хемраев
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 15 октября 2025

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

Получить навыки работы с контекстом безопасности и политиками SELinux.

# Ход выполнения работы

## Проверка состояния SELinux

- Активна политика **targeted**, режим **enforcing**

![Проверка состояния SELinux](Screenshot_1.png){ #fig:001 width=70% }

## Переключение режимов SELinux

- Перевод в режим **Permissive** (`setenforce 0`)
- Редактирование `/etc/sysconfig/selinux`: параметр `SELINUX=disabled`

![Отключение SELinux](Screenshot_2.png){ #fig:002 width=70% }

## Повторное включение SELinux

- Установлено значение `SELINUX=enforcing`
- После перезагрузки запущен процесс **релабелинга**

![Восстановление SELinux](Screenshot_5.png){ #fig:003 width=70% }

# Восстановление контекста безопасности

## Проверка и исправление контекста /etc/hosts

- Проверен контекст безопасности файла `/etc/hosts`
- Восстановление выполнено командой `restorecon -v /etc/hosts`

![Восстановление контекста безопасности](Screenshot_6.png){ #fig:004 width=70% }

# Настройка контекста для веб-сервера

## Создание и настройка каталога /web


- Применён контекст **httpd_sys_content_t**  
- Восстановлены контексты через `restorecon -R -v /web`

![Отображение страницы веб-сервера](Screenshot_11.png){ #fig:005 width=70% }

# Работа с переключателями SELinux

## Изменение параметров для службы FTP

- Проверены текущие переключатели: `getsebool -a | grep ftp`
- Активирован **ftpd_anon_write** (временный и постоянный)

![Настройка переключателей SELinux для FTP](Screenshot_12.png){ #fig:006 width=70% }

# Заключение

## Вывод

В ходе работы изучены принципы функционирования и конфигурирования SELinux, выполнены практические действия по изменению режимов работы, восстановлению контекстов безопасности и настройке политик для различных сервисов.
