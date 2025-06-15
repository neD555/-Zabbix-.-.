Домашнее задание к занятию «Система мониторинга Zabbix»

Задание 1
Установите Zabbix Server с веб-интерфейсом.
Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
Требования к результаты
Прикрепите в файл README.md скриншот авторизации в админке.
Приложите в файл README.md текст использованных команд в GitHub.

Решение 1
# Установка Zabbix 6.0 LTS на Debian 11 с PostgreSQL и Apache

## Использованные команды

```bash
# Обновление системы и установка PostgreSQL
sudo apt update
sudo apt install -y postgresql

# Установка репозитория Zabbix 6.0
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian11_all.deb
sudo dpkg -i zabbix-release_latest_6.0+debian11_all.deb
sudo apt update

# Установка серверной и веб-части Zabbix
sudo apt install -y zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts

# Создание пользователя и базы данных PostgreSQL
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix

# Импорт схемы базы данных
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

# Указание пароля к базе данных в конфиге Zabbix
sudo nano /etc/zabbix/zabbix_server.conf
# → Найти строку DBPassword= и указать:
# DBPassword=ваш_пароль

# Запуск и включение служб
sudo systemctl restart zabbix-server apache2
sudo systemctl enable zabbix-server apache2


![Задание1(2)Забикс](https://github.com/user-attachments/assets/11dd036d-915b-4b1a-bf42-2cf15574dd5c)
![Задание1(3)Забикс](https://github.com/user-attachments/assets/b3946c8c-32a5-43dd-abb9-e8eadb5a2ade)
