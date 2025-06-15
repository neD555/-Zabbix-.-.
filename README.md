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
![Задание1(2)Забикс](https://github.com/user-attachments/assets/072f1c7f-2fa4-40c3-b4a9-fd9f2c1da63b)
![Задание1(3)Забикс](https://github.com/user-attachments/assets/ec0e2ad2-fde0-4d56-a08f-0b3a0f3993f0)
# Установка Zabbix 6.0 LTS на Debian 11

## Использованные команды

```bash
sudo apt update
sudo apt install -y postgresql
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_6.0+debian11_all.deb
sudo dpkg -i zabbix-release_latest_6.0+debian11_all.deb
sudo apt update
sudo apt install -y zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sudo nano /etc/zabbix/zabbix_server.conf  # DBPassword=ваш_пароль
sudo systemctl restart zabbix-server apache2
sudo systemctl enable zabbix-server apache2
