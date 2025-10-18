---
## Front matter
lang: ru-RU
title: Лабораторная работа №7
subtitle: Управление журналами событий в системе
author:
  - Максат Хемраев
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 2 октября 2025

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

Получить навыки работы с журналами мониторинга различных событий в системе Linux.

# Ход выполнения работы

## Мониторинг системных событий

- Запуск мониторинга через `tail -f /var/log/messages`
- Проверка ошибок при вводе неверного пароля
- Использование команды `logger` для записи сообщений

![Мониторинг системных сообщений](Screenshot_1.png){ #fig:001 width=70% }

## Проверка безопасности

- Анализ файла /var/log/secure
- Отображение сообщений об ошибках авторизации

![Проверка журнала secure](Screenshot_3.png){ #fig:002 width=70% }

## Настройка rsyslog

- Установка и запуск Apache
- Перенаправление ошибок httpd через syslog
- Создание правила `local1.*` для /var/log/httpd-error.log

![Редактирование httpd.conf](Screenshot_6.png){ #fig:003 width=70% }

## Логи Apache через rsyslog

- Перезапуск служб rsyslog и httpd
- Создание отдельного файла для ошибок Apache
- Проверка записи в /var/log/httpd-error.log

![Создание правила для httpd](Screenshot_7.png){ #fig:004 width=70% }

## Отладочные сообщения

- Создание debug.conf с правилом *.debug
- Просмотр отладочных сообщений в messages-debug
- Отправка тестового сообщения через logger

![Проверка отладочного сообщения](Screenshot_9.png){ #fig:005 width=70% }

## Использование journalctl

- Просмотр журналов после загрузки системы
- Режим реального времени через `journalctl -f`
- Фильтрация по UID, приоритету и диапазону времени

![Просмотр журнала systemd](Screenshot_10.png){ #fig:006 width=70% }

## Фильтрация журналов

- Вывод в режиме verbose
- Анализ событий службы sshd

![Фильтрация по sshd](Screenshot_19.png){ #fig:007 width=70% }

## Постоянный журнал journald

- Создание каталога /var/log/journal
- Настройка прав доступа
- Перезапуск journald для активации

![Просмотр постоянного журнала](Screenshot_20.png){ #fig:008 width=70% }

# Итоги работы

## Вывод
В ходе работы были изучены:
- Основы журналирования в Linux
- Методы настройки rsyslog и journald
- Фильтрация и просмотр системных сообщений
- Создание постоянного журнала и разделение логов по уровням важности
