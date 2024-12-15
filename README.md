### OTUS High Load Lesson #05 | Subject: ISCSI, multipath и кластерные файловые системы: GFS2 
---------------------------
### ЦЕЛЬ: Реализация GFS2 хранилища 
---------------------------
### ВЫПОЛНЕНИЕ

Стенд состоит из 3 виртуальных машин: 
1. одна виртуальная машина, на которой расшариваем диск по ISCSI с файловой системой GFS2. Имя виртуальной машины - `iscsi`
2. три виртуальных машины, собранны в кластер, которые будут получать совместный доступ к iscsi-диску

Стенд разворачивается с помощью Terraform. В процессе развёртывания создается и запускается Ansible playbook, который выполняет необходимые настройки.

На виртуальных машинах используется операционная система __Ubuntu 24.04__

Для настройки ISCSI сервера Ansible использует bash скрипт, который генерируется в процессе выполнения terraform манифеста.

Используются следующие переменные:

`cluster_size` - количество машины, из которых состоит кластер
`cluster_instance_name` - имя инстансов кластера, а также имя самого кластера. Например, если указана переменная mycluster, будет собран кластер с названием "mycluster", и три члена кластера "mycluster[1,2,3]"
`system_user` - пользователь для подключения к виртуальным машинам
`iqn_base` - база iqn, с которой будут строиться iqn сервера и iqn клиентов
`vg_name` - название VG, который будет создан поверх iscsi диска
`lv_name` - название LV, который будет создан поверх iscsi диска
`fs_name` - название файловой системы GFS2, которая буде создана поверх iscsi диска
