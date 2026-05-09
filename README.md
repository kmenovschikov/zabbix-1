# Домашнее задание к занятию "`Zabbix - Часть 1`" - `Меновщиков Константин`


### Инструкция по выполнению домашнего задания

1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и вашу фамилию и имя
   - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
   - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
   - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1
Установите Zabbix Server с веб-интерфейсом.

##### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

##### Требования к результатам

- Прикрепите в файл README.md скриншот авторизации в админке.  
- Приложите в файл README.md текст использованных команд в GitHub.  

### Решение

1. sudo apt update
2. sudo apt install postresql
3. wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.0+debian12_all.deb
4. dpkg -i zabbix-release_latest_7.0+debian12_all.deb
5. sudo dpkg -i zabbix-release_latest_7.0+debian12_all.deb
6. sudo apt update
7. sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts
8. sudo -u postgres createuser --pwprompt zabbix
9. sudo -u postgres createdb -O zabbix zabbix
10. zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
11. sudo nano /etc/zabbix/zabbix_server.conf (отредактировать DBPassword)
12. systemctl restart zabbix-server apache2

<img width="2557" height="1134" alt="2026-05-09_09-01-19" src="https://github.com/user-attachments/assets/f267430e-b194-45df-83e2-8b541e0d45b3" />

---

### Задание 2 

Установите Zabbix Agent на два хоста.

#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

#### Требования к результатам
1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
4. Приложите в файл README.md текст использованных команд в GitHub

### Решение

1. wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.0+debian12_all.deb
2. sudo dpkg -i zabbix-release_latest_7.0+debian12_all.deb
3. sudo apt update
4. sudo apt install zabbix-agent
5. sudo nano /etc/zabbix/zabbix_agentd.conf (редактируем Server=)
6. sudo systemctl restart zabbix-agent

<img width="2559" height="1134" alt="2026-05-09_11-22-56" src="https://github.com/user-attachments/assets/5c365e9e-c238-4e68-a3cb-3ce93d34d673" />  
<br>
<img width="2559" height="1133" alt="2026-05-09_11-23-14" src="https://github.com/user-attachments/assets/d7bc58f8-1105-4363-8f62-4bb635dc4553" />
<br>
<img width="2559" height="1135" alt="2026-05-09_11-23-27" src="https://github.com/user-attachments/assets/a50fdca8-6f2d-4eb2-9acb-0b5e78a27f78" />

