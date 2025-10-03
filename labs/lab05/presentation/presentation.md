---
## Front matter
lang: ru-RU
title: Лабораторная работа №5
subtitle: Управление системными службами
author:
  - Максат Хемраев
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 21 сентября 2025

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

Получить навыки управления системными службами операционной системы посредством **systemd**.

# Ход выполнения работы

## Проверка службы vsftpd

- Получены права администратора  
- Проверен статус службы **vsftpd**  
- Сервис отсутствует в системе  

![Проверка статуса службы vsftpd](Screenshot_1.png){ #fig:001 width=70% }

## Установка vsftpd

- Установлен пакет **vsftpd** через dnf  
- Установка завершена успешно  

![Установка пакета vsftpd](Screenshot_1.png){ #fig:002 width=70% }

## Запуск vsftpd

- Служба **vsftpd** запущена  
- Проверка статуса: сервис активен, но отключён в автозагрузке  

![Запуск и проверка службы vsftpd](Screenshot_2.png){ #fig:003 width=70% }

## Автозапуск vsftpd

- Добавлен в автозапуск (enabled)  
- Затем удалён из автозапуска (disabled)  
- Проверка статуса подтвердила изменения  

![Добавление и удаление службы из автозапуска](Screenshot_3.png){ #fig:004 width=70% }  

## Символические ссылки vsftpd

- Просмотрены ссылки в каталоге systemd  
- При отключённом автозапуске ссылки нет  
- После включения автозапуска ссылка создана  

![Символические ссылки vsftpd](Screenshot_5.png){ #fig:006 width=70% }

## Зависимости vsftpd

- Проверены зависимости юнита **vsftpd**  
- Сервис запускается в рамках multi-user.target  
- Также просмотрены обратные зависимости  

![Зависимости службы vsftpd](Screenshot_6.png){ #fig:007 width=70% }

## Установка iptables

- Установлен пакет **iptables** и модули  
- Завершено успешно  

![Установка iptables](Screenshot_7.png){ #fig:008 width=70% }

## Проверка firewalld и iptables

- Статус firewalld: активен  
- Статус iptables: установлен, но неактивен  

![Проверка статуса firewalld и iptables](Screenshot_8.png){ #fig:009 width=70% }

## Конфликт сервисов

- При запуске **firewalld** iptables отключается  
- При запуске **iptables** firewalld останавливается  

![Запуск и остановка конфликтующих сервисов](Screenshot_9.png){ #fig:010 width=70% }

## Анализ юнитов

- В файле **firewalld.service** указано: Conflicts=iptables.service  

![Файл firewalld.service](Screenshot_10.png){ #fig:011 width=70% }  

## Анализ юнитов

- В iptables.service нет явного конфликта  

![Файл iptables.service](Screenshot_11.png){ #fig:012 width=70% }

## Маскирование iptables

- Остановлен iptables  
- Замаскирован с помощью systemctl mask  
- Создана ссылка на /dev/null  

![Замаскированный сервис iptables](Screenshot_12.png){ #fig:013 width=70% }

## Изолируемые цели

- Определён список изолируемых целей через AllowIsolate=yes  

![Список изолируемых целей](Screenshot_13.png){ #fig:014 width=70% }

## Изменение цели по умолчанию

- Цель по умолчанию: graphical.target  
- Изменена на multi-user.target (текстовый режим)  

![Изменение цели по умолчанию](Screenshot_14.png){ #fig:015 width=70% }

## Возврат к графическому режиму

- После перезагрузки система запустилась в текстовом режиме  
- Цель изменена обратно на graphical.target  
- ОС снова загрузилась с графическим интерфейсом  

![Возврат к графической цели по умолчанию](Screenshot_15.png){ #fig:016 width=70% }

# Заключение

- Изучены механизмы управления системными службами  
- Освоено добавление и удаление сервисов из автозапуска  
- Рассмотрены конфликты между iptables и firewalld  
- Получены навыки работы с изолируемыми целями и установкой цели по умолчанию
