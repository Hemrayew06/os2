---
## Front matter
lang: ru-RU
title: Лабораторная работа №11
subtitle: Управление загрузкой системы (GRUB2)
author:
  - Максат Хемраев
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 26 октября 2025

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

Получить навыки работы с загрузчиком системы **GRUB2**, его конфигурацией и методами восстановления системы.

# Ход выполнения работы

## Модификация параметров GRUB2

- Изменён параметр **GRUB_TIMEOUT=10**
- Сохранён файл и обновлена конфигурация загрузчика

![Редактирование файла grub](Screenshot_1.png){ #fig:001 width=70% }

## Генерация нового файла конфигурации

- Выполнена команда `grub2-mkconfig > /boot/grub2/grub.cfg`
- После перезагрузки появилось меню **GRUB 2.12**

![Меню загрузчика GRUB](Screenshot_3.png){ #fig:002 width=70% }

## Загрузка в режиме восстановления (rescue)

- В меню GRUB нажата клавиша **e**  
- Добавлен параметр *systemd.unit=rescue.target*
- Загружена базовая системная среда

![Загруженные модули в режиме rescue](Screenshot_5.png){ #fig:003 width=70% }

## Просмотр окружения системы

- Выведены активные модули с помощью *systemctl list-units*
- Проверены переменные среды через *systemctl show-environment*

![Просмотр переменных окружения](Screenshot_5.png){ #fig:004 width=70% }

## Загрузка в аварийном режиме (emergency)

- В конце строки ядра добавлен параметр *systemd.unit=emergency.target*
- Загружена минимальная системная среда

![Аварийный режим загрузки](Screenshot_7.png){ #fig:005 width=70% }

## Сброс пароля пользователя root

- При загрузке добавлен параметр *rd.break*
- Попытка смены пароля завершилась ошибкой из-за недоступности утилит

![Попытка сброса пароля root](Screenshot_9.png){ #fig:006 width=70% }

# Итоги работы

## Вывод

В ходе лабораторной работы изучены:
- Принципы настройки загрузчика **GRUB2**  
- Методы восстановления системы в режимах *rescue* и *emergency*  
- Процесс сброса пароля суперпользователя **root**  
