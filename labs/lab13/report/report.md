---
## Front matter
title: "Отчёт по лабораторной работе №13"
subtitle: "Фильтр пакетов"
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

Получить навыки настройки пакетного фильтра в Linux.

# Отчёт по выполнению работы

## Управление брандмауэром с использованием `firewall-cmd`

1. Получил права суперпользователя и определил зону по умолчанию.  
   Команда вывела значение **public**, что означает применение стандартных правил для входящих подключений.

2. Просмотрел доступные зоны и перечень служб, которые могут быть добавлены в правила брандмауэра.  
   Вывод показал большое количество предустановленных сервисов.

   ![Список зон и служб](Screenshot_1.png){ #fig:001 width=80% }

3. Затем проверил, какие службы разрешены в текущей зоне.  
   Команда `firewall-cmd --list-services` показала активные разрешённые сервисы — `cockpit`, `dhcpv6-client`, `ssh`.

   ![Список разрешённых служб](Screenshot_2.png){ #fig:002 width=80% }

4. Сравнил вывод команд `firewall-cmd --list-all` и `firewall-cmd --list-all --zone=public`.  
   Результаты совпали, что подтверждает — активная зона действительно **public**.

5. Добавил службу **vnc-server** во временную конфигурацию (в runtime).  
   Проверка показала, что служба появилась в списке разрешённых.

   ![Добавление vnc-server](Screenshot_3.png){ #fig:003 width=80% }

6. Перезапустил службу `firewalld`.  
   После перезапуска **vnc-server исчез из конфигурации**.  
   Это происходит потому, что добавление было выполнено только во *временной (runtime)* конфигурации, а перезапуск сбросил её до значений *постоянной (permanent)*.

7. Повторно добавил службу **vnc-server**, но уже в постоянную конфигурацию: `firewall-cmd --add-service=vnc-server --permanent`

После команды `firewall-cmd --reload` служба появилась и в runtime-конфигурации.

![vnc-server добавлен permanent](Screenshot_4.png){ #fig:004 width=80% }

8. Добавил порт **2022/tcp** в постоянную конфигурацию, затем перегрузил её.  
Проверка `firewall-cmd --list-all` показывает порт в списке разрешённых.

![Добавление порта 2022/tcp](Screenshot_5.png){ #fig:005 width=80% }

---

## Управление брандмауэром с использованием графического интерфейса `firewall-config`

1. Запустил утилиту `firewall-config`.  
Переключил параметр **Configuration → Permanent**, чтобы изменения сохранялись на диске.

2. В зоне **public** включил службы **http**, **https**, **ftp**.

![Включение служб в GUI](Screenshot_6.png){ #fig:006 width=80% }

3. На вкладке *Ports* добавил порт **2022/udp**.

![Добавление порта 2022/udp](Screenshot_7.png){ #fig:007 width=80% }

4. После внесения изменений выполнил: `firewall-cmd --reload`

Теперь в конфигурации времени выполнения отображаются как службы, так и новый порт.

![Синхронизация постоянной и runtime конфигурации](Screenshot_8.png){ #fig:008 width=80% }

---

## Самостоятельная работа

1. Конфигурация межсетевого экрана должна разрешать службы:
- **telnet** — добавлено через команду CLI:
  ```
  firewall-cmd --add-service=telnet --permanent
  firewall-cmd --reload
  ```
- **imap**, **pop3**, **smtp** — добавлены через GUI (`firewall-config`) во вкладке *Services* для зоны **public**.

2. Проверка конфигурации:

![Проверка конфигурации](Screenshot_9.png){ #fig:009 width=80% }

# Контрольные вопросы

### 1. Какая служба должна быть запущена перед началом работы с менеджером конфигурации брандмауэра firewall-config?
Для работы утилиты **firewall-config** должна быть запущена служба `firewalld`.

---

### 2. Какая команда позволяет добавить UDP-порт 2355 в конфигурацию брандмауэра в зоне по умолчанию?
Используется команда: `firewall-cmd --add-port=2355/udp --permanent`.

---

### 3. Какая команда позволяет показать всю конфигурацию брандмауэра во всех зонах?
Команда: `firewall-cmd --list-all-zones`.

---

### 4. Какая команда позволяет удалить службу vnc-server из текущей конфигурации брандмауэра?
Удаление выполняется командой: `firewall-cmd --remove-service=vnc-server`.

---

### 5. Какая команда firewall-cmd позволяет активировать новую конфигурацию, добавленную опцией --permanent?
Активация выполняется командой: `firewall-cmd --reload`.

---

### 6. Какой параметр firewall-cmd позволяет проверить, что новая конфигурация была добавлена в текущую зону и теперь активна?
Для просмотра используется команда: `firewall-cmd --list-all`.

---

### 7. Какая команда позволяет добавить интерфейс eno1 в зону public?
Команда: `firewall-cmd --zone=public --change-interface=eno1 --permanent`.

---

### 8. Если добавить новый интерфейс в конфигурацию брандмауэра, пока зона не указана, в какую зону он будет добавлен?
Интерфейс будет добавлен в **зону по умолчанию**, чаще всего это `public`.

---


# Заключение

В ходе работы были изучены команды и инструменты для управления брандмауэром firewalld, включая добавление служб и портов как во временную, так и в постоянную конфигурацию, а также применение изменений через firewall-config.
