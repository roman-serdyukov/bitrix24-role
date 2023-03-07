Install Bitrix 24
=========
install_bitrix24.yml

Ansible role для подготовкики сервера к развертыванию "1С-Битрикс24 коробочная версия" (также подойдет и для "1С-Битрикс: Управление сайтом"). Написана в соответсвии с [инструкцией](https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=135&CHAPTER_ID=04495&LESSON_PATH=10495.4495) для Ubuntu 22.04, Debian 11, CentOS 7.
Состоит из следующих групп tasks:
- Установка locales RU - install_locale_ru.yml.
- Установка «1С-Битрикс: Веб-окружение» - Linux (BitrixEnv) на CentOS 7 - install_for_centos7.yml
  + Может включать в себя task по монтированию отдлельного раздела /dev/vdb для файлов bitrix - mount_part.yml.
- Установка необходимых пакетов для Ubuntu 22.04, Debian 11 - install_pack.yml.
- Первоначальное конфигурирование, скачивание пакетов с конфигурациями для Ubuntu 22.04, Debian 11 - preconfig_pack.yml.
- Настройка nginx для Ubuntu 22.04, Debian 11 - config_nginx.yml.
- Настройка php для Ubuntu 22.04, Debian 11 - config_php.yml.
- Настройка apache для Ubuntu 22.04, Debian 11 - config_apache.yml.
- Настройка mariadb для Ubuntu 22.04, Debian 11 - config_mariadb.yml.
- Настройка redis для Ubuntu 22.04, Debian 11 - config_redis.yml.
- Настрйока push-server для Ubuntu 22.04, Debian 11 - config_push-server.yml.
- Настройка сайта для Ubuntu 22.04, Debian 11 - config_site.yml
  + Может включать в себя task для копирования файлов предустановок сайта - preset_site.yml.
  + Может включать в себя task по монтированию отдлельного раздела /dev/vdb для файлов bitrix - mount_part.yml.
Включить/отключить нужный блок можно раскоментировав/закоментировав его в tasks/main.yml

Requirements
------------

- Ansible 2.13.3
- Python 3.10.6
- Работоспособность протестирована на Ubuntu 22.04, Debian 11, CentOS 7.

Role Variables
--------------

+ other_pack:           список пакетов для установки
+ php_repo_ubuntu:      репозиторий рhp для Ubuntu
+ php_url_debian:       ссылка на репозиторий php для  Debian
+ php_pack:             список пакетов php для установки
+ settings_url:         ссылка для скачивания файла с настройками для систем Debian
+ dist_file:            файл автоматической настройки BitrixEnv на CentOS 7 (bitrix-env-crm.sh - для "1С-Битрикс24 коробочная версия", bitrix-env.sh - для "1С-Битрикс: Управление сайтом")
+ bitrix_env_url:       ссылка на скачивание файла автоматической настройки BitrixEnv на CentOS 7 + название дистрибутива (см. переменную выше)
+ dest_folder:          папка назначения для скачивания
+ server_name:          имя сервера
+ mysql_ver:            версия mysql
+ pushserver_url:       ссылка для скачивания push-server
+ bitrixsetup_url:      ссылка для скачаивания bitrixsetup.php
+ mysql_db:             имя базы данных
+ mysql_user:           имя пользователя базы данных
+ mysql_host:           имя хоста базы данных
+ second_fs:            файловая система для дополнительного диска /dev/vdb

Следующие переменные указывал в group_vars:
+ mysql_root_password:  пароль mysql для root
+ mysql_pass:           пароль mysql для создаваемого пользователя БД
+ security_key:         security_key для push-server

Example Playbook
----------------
```
- name: Install postgresql 14 for server 1C
  hosts: your_servers
  roles:
    - install_bitrix24.yml
```
  
License
-------

MIT

Author Information
------------------

Сердюков Роман <br>
reserdukov@gmail.com
