# Лабораторная работа № 3.

## Содержание

1. [Цели работы](#цели-работы)
2. [Требования к сдаче работы](#требования-к-сдаче-работы)
3. [Утилиты диагностики TCP/IP](#утилиты-диагностики-tcpip)
4. [Ход работы](#ход-работы)
5. [Задания](#задания)
6. [Контрольные вопросы](#контрольные-вопросы)



## Тема: Настройка параметров сетевого соединения в Cisco Packet Tracer 6.2

### Цели работы:

*  научиться работать с программой Cisco Packet Tracer;
*  научиться настраивать сетевые параметры;
*  изучить утилиты диагностики TCP/IP.

Для успешного решения задач администрирования необходимо хорошо разбираться в системе IP-адресации. Знание принципов использования масок и структуризации сетей поможет грамотно решать многие вопросы настройки локальной сети.

---

## Требования к сдаче работы

Работа офорляется в тетради. Нужно записать номер работы, тему и цели.
Записать информацию об утилитах диагностики TCP/IP

***Критерии оценивания***

* Оценка 5 - Переписать информацию об утилитах. Просмотреть видеоуроки, создать сети и протестировать работу сетей согласно примерам из видео, ответить устно на все контрольные вопросы.
* Оценка 4 - Переписать информацию об утилитах. Просмотреть видеоуроки, создать сети и протестировать работу сетей согласно примерам из видео, ответить устно на четыре любых контрольных вопроса.
* Оценка 3 - Переписать информацию об утилитах. Просмотреть видеоуроки, создать сети и протестировать работу сетей согласно примерам из видео, ответить устно на два любых контрольных вопроса.



## Утилиты диагностики TCP/IP

В состав большинства операционных систем входит ряд утилит (небольших программ), 
предназначенных для диагностики функционирования стека TCP/IP. 
Каждый системный администратор должен знать эти утилиты и уметь применять их на практике.
Информацию о любой утилите можно вывести,
набрав в командной строке `имя утилиты с ключом «/?»`, например: `ipconfig /?`

### IPconfig

Утилита предназначена, во-первых, для вывода информации о конфигурации стека TCP/IP, во-вторых, для выполнения некоторых действий по настройке стека.
При вводе названия утилиты в командной строке без параметров на экране отобразится информация об основных настройках TCP/IP:

- суффикс DNS (Connection-specific DNS Suffix);
- IP-адрес (IP Address);
- маска подсети (Subnet Mask);
- шлюз по умолчанию (Default Gateway).

Приведем основные ключи утилиты:
* `/all` – отображение полной информации о настройке стека TCP/IP на данном компьютере. Следует отметить, что при наличии нескольких сетевых адаптеров выводятся данные по каждому адаптеру отдельно. Наиболее важные сведения кроме представленных выше – физический адрес (МАС-адрес) сетевого адаптера (Physical Address) и наличие разрешения DHCP (DHCP Enabled).
* `/release` – освобождение IP-адреса (имеет смысл, если DHCP разрешен).
* `/renew` – обновление конфигурации TCP/IP (обычно выполняется, если DHCP разрешен).
* `/displaydns` – вывод на экран кэша имен DNS.
* `/flushdns` – очистка кэша имен DNS.
* `/registerdns` – обновление аренды DHCP и перерегистрация доменного имени в базе данных службы DNS

### Ping

Основная цель этой популярной утилиты – **выяснение возможности установления соединения с удаленным узлом.** 
Кроме того, утилита может обратиться к удаленному компьютеру по доменному имени, 
чтобы проверить способность преобразования символьного доменного имени в IP-адрес.

Принцип работы: утилита отправляет на удаленный узел несколько пакетов (число пакетов определяется ключом –n, по умолчанию четыре) по протоколу ICMP. Такие пакеты называются эхо-пакетами, т. е. требуют ответа. Если удаленный узел доступен, он отвечает на каждый эхо-пакет своим пакетом, а утилита измеряет интервал между отправкой эхо-пакета и приходом ответа.
Нужно отметить, что отсутствие ответа может быть связано не с физической недоступностью удаленного компьютера, а с тем, что на нем установлено программное обеспечение, запрещающее отправку ответов на эхо-пакеты (брандмауэр – firewall).
Основные ключи:
* `–t`– пакеты отправляются до тех пор, пока пользователь не нажмет комбинацию CTRL+C.
* `–a`– определение доменного имени по IP-адресу.
* `–l <размер>` – максимальный размер пакета (по умолчанию 32 байта).
* `–w <таймаут>` – задание времени ожидания ответа в миллисекундах (по умолчанию 1000 миллисекунд = 1 секунда).

### Tracert

Название утилиты произошло от **Trace Route** – отслеживание маршрута. 
Утилита позволяет решить следующие задачи:

- проследить путь прохождения пакета от данного компьютера до удаленного узла (отображаются промежуточные узлы- маршрутизаторы);
- выявить участки задержки пакетов;
- выявить места потери пакетов.

Принцип работы: утилита отправляет эхо-пакеты на заданный удаленный узел. Отличие между эхо-пакетами заключается в параметре, который называется «время жизни» (TTL – Time To Live). Этот параметр обозначает количество маршрутизаторов (процесс перехода пакета через маршрутизатор называется hop – прыжок), которое может пройти пакет, прежде чем попадет на заданный узел. Каждый маршрутизатор уменьшает время жизни на единицу. Если на каком-то маршрутизаторе TTL станет равным нулю, тот отбрасывает пакет и отправляет служебное сообщение на узел-источник.
Первый эхо-пакет посылается с временем жизни, равным единице. Первый маршрутизатор отбрасывает эхо-пакет и отправляет служебное сообщение, в котором содержится информации об имени и адресе маршрутизатора. Следующий эхо-пакет имеет TTL = 2 и отбрасывается уже
на втором маршрутизаторе. Таким образом, эхо-пакеты отправляются с увеличением времени жизни на единицу, пока не придет ответ от заданного удаленного узла или время ожидания не будет превышено.
Основные ключи:

*  `/h <maximum_hops>` – максимальное число хопов (маршрутизаторов) при поиске узла.
*  `/w <таймаут>` – задание времени ожидания ответа в миллисекундах.

### netstat

Утилита отображает статистическую информацию по протоколам IP, TCP, UDP и ICMP, а также позволяет отслеживать сетевые соединения.
Основные ключи:
* `/a` – список всех подключений и прослушивающихся портов.
* `/e` – статистика для Ethernet.
* `/n`– список всех подключений и портов в числовом формате.
* `/s` – статистика для перечисленных четырех протоколов.
* `<interval>` – интервал в секундах, через который утилита выводит требуемую информацию (для прекращения вывода – CTRL+C).

### arp

Эта утилита работает с протоколами преобразования IP-адресов в МАС-адреса и обратно ARP и RARP. С её помощью можно выводить на экран таблицу соответствия IP-адресов и МАС-адресов (ARP-кэш), добавлять и удалять записи в ней.
Основные ключи:
*  `/a` – отображение таблицы ARP или, если указан IP-адрес, запись
только для этого адреса.
*  `/s` – добавление записи в таблицу.
*  `/d` – удаление записи из таблицы.

### hostname
Это самая простая утилита – она выводит на экран имя компьютера.


## Ход работы
Просмотрите видео по работе с программой Cisco Packet Tracer

### [Архив с программой](https://drive.google.com/file/d/1-RJz5lQXm8VzllBU_PdR7hPh9steNxr4/view?usp=drive_link)
В первом видео подробно указано как установить программу.
Создайте и настройте сети как по образцу из видео 2 и 3

1. [1.Видео уроки Cisco Packet Tracer. Курс молодого бойца. Установка](https://www.youtube.com/watch?v=sEqQrE38M58&list=PLcDkQ2Au8aVNYsqGsxRQxYyQijILa94T9&index=2)
2. [2.Видео уроки Cisco Packet Tracer. Курс молодого бойца. Простейшая сеть](https://www.youtube.com/watch?v=c9TMXiRk3E8&list=PLcDkQ2Au8aVNYsqGsxRQxYyQijILa94T9&index=3)
3. [3.Видео уроки Cisco Packet Tracer. Курс молодого бойца. Коммутатор](https://www.youtube.com/watch?v=VZDvaleQB0s&list=PLcDkQ2Au8aVNYsqGsxRQxYyQijILa94T9&index=4)

## Задания

1. Изучите возможности утилиты ping.
2. Изучите возможности утилиты tracert.
3. Исследуйте возможности утилиты netstat.

### Контрольные вопросы
1. Выпишите основные утилиты диагностики TCP/IP. Назначение утилиты, основные параметры.
2. Как узнать физический адрес компьютера?
3. Нужно ли перезапускать компьютер, чтобы изменения вступили в силу, если изменяются следующие параметры:
    ◦ настройки стека TCP/IP;
    ◦ имя рабочей группы;
    ◦ имя компьютера?
4. Как с помощью утилиты ping определить достижимость узла? Какая информация, полученная при использовании утилиты ping, служит ответом о достижимости узла?
5. Как определить IP-адрес удаленного узла, зная только его символьное имя?
6. Как изменить размер пакета утилиты ping?
7. Параметры свойств протокола TCP/IP компьютера локальной сети были настроены вручную. После этого компьютер может устанавливать соединение с любым компьютером внутренней сети, но компьютеры удаленной подсети остаются недостижимыми. Объясните, в чем проблема и как ее устранить.
8. Какая утилита определяет имя узла?