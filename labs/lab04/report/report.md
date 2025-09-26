---
## Front matter
title: "Отчёт по лабораторной работе №4"
subtitle: "Работа с программными пакетами"
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

Получить навыки работы с репозиториями и менеджерами пакетов.

# Отчёт по выполнению работы  

## Работа с репозиториями  

1. Вошёл в систему под пользователем **root** и перешёл в каталог **/etc/yum.repos.d**. Изучил доступные файлы конфигурации репозиториев, среди которых:  
   - *rocky-addons.repo*  
   - *rocky-devel.repo*  
   - *rocky-extras.repo*  
   - *rocky.repo*  

   Содержимое файла *rocky-extras.repo* подтверждает наличие настроенного зеркала для получения дополнительных пакетов.  

   ![Файл rocky-extras.repo](Screenshot_1.png){ #fig:001 width=80% }  

2. Вывел список доступных репозиториев с помощью команды **dnf repolist**. Система определила активные репозитории:  
   - *AppStream* — дополнительные пакеты приложений,  
   - *BaseOS* — базовые компоненты системы,  
   - *Extras* — дополнительные пакеты и утилиты.  

   ![Список репозиториев](Screenshot_2.png){ #fig:002 width=80% }  

3. Выполнил поиск пакетов, содержащих слово **user** в названии или описании. Были найдены библиотеки и утилиты, связанные с управлением пользователями и пользовательскими каталогами (например, *libuser*, *usermode*, *xdg-user-dirs*).  

4. Провёл поиск и изучение пакета **nmap**. Получил информацию о версии, размере, назначении и репозитории, из которого он доступен (*AppStream*).  

   ![Информация о пакете nmap](Screenshot_3.png){ #fig:003 width=80% }  

   - Команда **dnf install nmap** устанавливает только основной пакет.  
   - Команда **dnf install nmap\*** дополнительно устанавливает связанные компоненты (*nmap-ncat*).  

   ![Установка пакета nmap](Screenshot_4.png){ #fig:004 width=80% }  

5. Удалил установленный пакет **nmap** вместе с зависимостями, используя команды:  
   - `dnf remove nmap` — удаляет основной пакет,  
   - `dnf remove nmap\*` — удаляет все пакеты, связанные с nmap (в том числе *nmap-ncat*).  

   ![Удаление пакета nmap](Screenshot_5.png){ #fig:005 width=80% }  

6. Получил список групп пакетов. Среди доступных — *Development Tools*, *Security Tools*, *RPM Development Tools* и др.  

   ![Список групп пакетов](Screenshot_6.png){ #fig:006 width=80% }  

   Изучил описание группы **RPM Development Tools**, включающей утилиты для сборки RPM-пакетов (*rpm-build*, *redhat-rpm-config* и др.).  

   ![Информация о группе RPM Development Tools](Screenshot_7.png){ #fig:007 width=80% }  

   Установил группу командой **dnf groupinstall "RPM Development Tools"**, после чего в систему добавились пакеты *rpmdevtools* и *python3-argcomplete*.  

   Для удаления группы использовал команду **dnf groupremove "RPM Development Tools"**.  

   ![Удаление группы RPM Development Tools](Screenshot_8.png){ #fig:008 width=80% }  

7. Изучил историю операций DNF при помощи команды **dnf history**. Система сохранила последовательность установки и удаления пакетов и групп.  

   ![История DNF](Screenshot_9.png){ #fig:009 width=80% }  

   Отменил шестое действие из истории командой **dnf history undo 6**, а также проверил результат выполнения команды **dnf history undo 7**.  

---

## Использование rpm  

1. Скачал rpm-пакет **lynx** с помощью команд `dnf list lynx` и `dnf install lynx --downloadonly`.  
   Пакет был загружен в кэш DNF.  

   ![Загрузка пакета lynx](Screenshot_10.png){ #fig:010 width=80% }  

2. Определил каталог, куда был помещён загруженный пакет — **/var/cache/dnf/appstream.../packages**.  

3. Перешёл в данный каталог и установил пакет командой `rpm -Uhv lynx-2.9.0-6.el10.x86_64.rpm`.  
   После установки пакет стал доступен в системе.  

4. Проверил расположение исполняемого файла с помощью команды `which lynx`.  
   Результат — **/usr/bin/lynx**.  

   ![Исполняемый файл lynx](Screenshot_11.png){ #fig:011 width=80% }  

5. С помощью команды `rpm -qf $(which lynx)` убедился, что бинарный файл принадлежит пакету lynx.  
   Дополнительно получил сведения о пакете через команду `rpm -qi lynx`.  
   Информация содержит версию (2.9.0), архитектуру (x86_64), лицензию (GPL-2.0), URL и краткое описание.  

6. Получил список всех файлов пакета с помощью `rpm -ql lynx`.  
   Среди них: бинарные файлы, документация, служебные файлы.  

   Для просмотра документации выполнил `rpm -qd lynx`.  
   Были найдены файлы руководств и справочные материалы, включая **Lynx_users_guide.html**.  

   ![Файлы пакета lynx](Screenshot_12.png){ #fig:012 width=80% }  
   ![Документация пакета lynx](Screenshot_13.png){ #fig:013 width=80% }  

7. Вывел список конфигурационных файлов пакета с помощью команды `rpm -qc lynx`.  
   Результат — файлы `/etc/lynx.cfg`, `/etc/lynx-site.cfg`, `/etc/lynx.lss`.  

   ![Конфигурационные файлы lynx](Screenshot_14.png){ #fig:014 width=80% }  

8. Проверил наличие скриптов, выполняемых при установке, с помощью `rpm -q --scripts lynx`.  
   В данном случае специфических скриптов не было. Скрипты, если они есть, выполняют дополнительные действия при установке, удалении или обновлении пакета (например, настройка сервисов).  

9. Под своей учётной записью запустил текстовый браузер **lynx** и убедился в его работоспособности.  

10. Вернувшись в терминал **root**, удалил пакет командой `rpm -e lynx`.  
    После удаления пакет исчез из списка установленных.  

---

## Установка и изучение пакета dnsmasq  

1. Установил пакет **dnsmasq** с помощью команд `dnf list dnsmasq` и `dnf install dnsmasq`.  
   Проверил расположение исполняемого файла — он находится в каталоге **/usr/sbin/dnsmasq**.  

   ![Установка и определение расположения dnsmasq](Screenshot_15.png){ #fig:015 width=80% }  

2. С помощью команды `rpm -qf $(which dnsmasq)` подтвердил, что исполняемый файл принадлежит пакету **dnsmasq**.  
   Далее, командой `rpm -qi dnsmasq` получил полную информацию о пакете: версия (2.90), архитектура (x86_64), размер (794976 байт), лицензия (GPL-2.0-only), а также назначение — **легковесный DNS-, DHCP- и TFTP-сервер**.  

3. Вывел список всех файлов пакета с помощью команды `rpm -ql dnsmasq`.  
   Среди них присутствуют:  
   - бинарные файлы в **/usr/sbin**,  
   - системные юниты для systemd,  
   - документация в **/usr/share/doc/dnsmasq**.  

   Для вывода только файлов документации использовал `rpm -qd dnsmasq`. В список входят **FAQ**, **setup.html**, **COPYING** и другие справочные материалы.  

   ![Файлы пакета dnsmasq](Screenshot_16.png){ #fig:016 width=80% }  

4. С помощью команды `rpm -qc dnsmasq` получил список конфигурационных файлов пакета.  
   Основные:  
   - **/etc/dnsmasq.conf**  
   - **/etc/dnsmasq.d/**  

5. Изучил скрипты, выполняемые при установке пакета (`rpm -q --scripts dnsmasq`).  
   - *preinstall* — создаёт системного пользователя и группу **dnsmasq** для корректной работы сервиса.  
   - *postinstall* — регистрирует службу в systemd.  
   - *preuninstall* — удаляет службу при деинсталляции.  

   Эти скрипты автоматизируют настройку окружения для пакета.  

   ![Скрипты пакета dnsmasq](Screenshot_17.png){ #fig:017 width=80% }  

6. В завершение удалил пакет с помощью команды `rpm -e dnsmasq`.  


# Контрольные вопросы  

### 1. Какая команда позволяет вам искать пакет rpm, содержащий файл useradd?  
- `rpm -qf $(which useradd)` — определяет, к какому пакету относится файл.  
- Если нужно найти через базу: `dnf provides */useradd`.  

---

### 2. Какие команды вам нужно использовать, чтобы показать имя группы dnf, которая содержит инструменты безопасности и показать, что находится в этой группе?  
- `dnf group list` — список всех доступных групп.  
- `dnf group info "Security Tools"` — информация о содержимом группы *Security Tools*.  

---

### 3. Какая команда позволяет вам установить rpm, который вы загрузили из Интернета и который не находится в репозиториях?  
- `rpm -Uvh имя_пакета.rpm` — установка загруженного пакета.  
- Альтернативный вариант через dnf: `dnf install ./имя_пакета.rpm`.  

---

### 4. Вы хотите убедиться, что пакет rpm, который вы загрузили, не содержит никакого опасного кода сценария. Какая команда позволяет это сделать?  
- `rpm -qp --scripts имя_пакета.rpm` — показывает скрипты, выполняемые при установке и удалении пакета.  

---

### 5. Какая команда показывает всю документацию в rpm?  
- `rpm -qd имя_пакета` — выводит список всех файлов документации пакета.  

---

### 6. Какая команда показывает, какому пакету rpm принадлежит файл?  
- `rpm -qf /путь/к/файлу` — определяет пакет, которому принадлежит данный файл.  

---

# Заключение

В ходе работы были изучены команды **dnf** и **rpm** для установки, удаления и анализа пакетов, а также работы с репозиториями и групповыми установками. Полученные навыки позволяют администрировать программное обеспечение в Linux, контролировать зависимости и проверять безопасность устанавливаемых пакетов.  