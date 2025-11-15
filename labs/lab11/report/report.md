---
## Front matter
title: "Отчёт по лабораторной работе №11"
subtitle: "Управление загрузкой системы"
author: "Максат Хемраев"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true
toc-depth: 2
lof: true
lot: true
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
    - spelling=modern
    - babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float}
  - \floatplacement{figure}{H}
---

# Цель работы

Получить навыки работы с загрузчиком системы GRUB2.

# Отчёт по выполнению работы  

## Модификация параметров GRUB2  

1. В терминале была запущена сессия пользователя **mhemraev**. Для выполнения административных действий получены права суперпользователя.  

2. В текстовом редакторе **mcedit** был открыт файл конфигурации загрузчика — **/etc/default/grub**.  
   В параметре **GRUB_TIMEOUT** установлено значение *10*, задающее время отображения меню загрузки.  
   Также проверено наличие строк, отвечающих за настройки вывода и параметры запуска ядра.  

   ![Редактирование файла grub](Screenshot_1.png){ #fig:001 width=80% }

3. После сохранения изменений была выполнена команда генерации нового конфигурационного файла загрузчика.  
   Система подтвердила успешное создание конфигурации и добавление записи для UEFI.  

   ![Обновление конфигурации GRUB2](Screenshot_2.png){ #fig:002 width=80% }

4. После перезагрузки компьютера на экране появилось меню **GRUB version 2.12** с возможностью выбора ядра операционной системы.  

   ![Меню загрузчика GRUB](Screenshot_3.png){ #fig:003 width=80% }

---

## Загрузка в режиме восстановления  

1. Для входа в режим восстановления выбрана строка с текущей версией ядра, после чего нажата клавиша **e** для редактирования параметров загрузки.  

   ![Редактирование параметров ядра](Screenshot_4.png){ #fig:004 width=80% }

2. В конце строки, начинающейся с *linux*, добавлен параметр *systemd.unit=rescue.target*.  
   После этого загрузка продолжена с помощью сочетания клавиш **Ctrl + X**.  

3. После входа в систему подтверждено, что загружена базовая среда восстановления.  
   Командой *systemctl list-units* был просмотрен список активных модулей.  

   ![Загруженные модули в режиме rescue](Screenshot_5.png){ #fig:005 width=80% }

4. С помощью команды *systemctl show-environment* выведены переменные окружения текущей сессии.  

---

## Загрузка в аварийном режиме  

1. После перезагрузки система вновь остановлена в меню GRUB.  
   При редактировании строки загрузки ядра был добавлен параметр *systemd.unit=emergency.target*.  

   ![Редактирование строки для аварийного режима](Screenshot_6.png){ #fig:006 width=80% }

2. После запуска в аварийном режиме команда *systemctl list-units* показала минимальный набор активных модулей, характерный для среды **emergency**.  

   ![Минимальный набор активных модулей](Screenshot_7.png){ #fig:007 width=80% }

---

## Сброс пароля пользователя root  

1. Для восстановления пароля выполнена загрузка в режиме редактирования параметров ядра.  
   В конце строки, загружающей ядро, добавлен параметр *rd.break*.  

   ![Добавление параметра rd.break](Screenshot_8.png){ #fig:008 width=80% }

2. После загрузки система перешла в оболочку **initramfs** до монтирования корневой файловой системы.  
   Командой *mount -o remount,rw /sysroot* предоставлен доступ на запись.  

3. Переход в корневую среду был выполнен командой *chroot /sysroot*.  
   После чего вызов команды *passwd* не был найден — ошибка указывает на отсутствие необходимых утилит на данном этапе загрузки.  

   ![Попытка сброса пароля root](Screenshot_9.png){ #fig:009 width=80% }

---

# Контрольные вопросы  

### 1. Какой файл конфигурации следует изменить для применения общих изменений в GRUB2?  
- `/etc/default/grub` — основной файл конфигурации, в котором задаются параметры загрузчика GRUB2, такие как таймаут, параметры ядра и режим отображения меню.  

### 2. Как называется конфигурационный файл GRUB2, в котором вы применяете изменения для GRUB2?  
- `/boot/grub2/grub.cfg` — итоговый конфигурационный файл, используемый загрузчиком при старте системы. Он формируется автоматически на основе настроек из `/etc/default/grub`.  

### 3. После внесения изменений в конфигурацию GRUB2, какую команду вы должны выполнить, чтобы изменения сохранились и воспринялись при загрузке системы?  
- `grub2-mkconfig > /boot/grub2/grub.cfg` — команда для генерации нового конфигурационного файла GRUB2 с учётом внесённых изменений.  

---

# Заключение  

В ходе работы были изучены принципы конфигурации загрузчика GRUB2, способы изменения его параметров и методы восстановления системы через режимы *rescue* и *emergency*.  
Также был рассмотрен процесс сброса пароля пользователя **root** с использованием параметра *rd.break* и минимальной среды загрузки.  
