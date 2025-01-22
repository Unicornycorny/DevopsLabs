## **Ход работы**

1. Развернуть виртуальную машину для приложения (app) и виртуальную машину для будущей системы базы данных (db) через Vagrantfile
2. Написать роль установки **PostgreSQL** и плейбук, который ее разворачивает
3. Все параметры должны быть вынесены в переменные, все переменные должны быть префиксованы, значения переменных устанавливаются через group_vars для плейбука, роль должна быть покрыта тестами
4. Добавить возможность смены директории с данными на кастомную
5. Добавить возможность создания баз данных и пользователей
6. ***Добавить функционал настройки streaming-репликации***
7. ***Продумать логику определения master и replica нод СУБД и их настройки при работе роли***

- Поднимаем машины:
```
vagrant up
vagrant status
```

- Инициализируем роль:
```
ansible-galaxy init postgresql-role
```
- Заполняем плейбук и переменные

```
---
- name: Setup Master
  hosts: master
  become: true

  tasks:
    - name: "Include pgsql for master role"
      include_role:
        name: postgres
      vars:
        postgres_role: master

- name: Setup Replica
  hosts: replica
  become: true

  tasks:
    - name: "Include pgsql for replica role"
      include_role:
        name: postgres
      vars:
        postgres_role: replica
```

- Заполяем postgres(пишем tasks, templates etc)
- Создаём molescule сценарий:

```
molecule init scenario --driver-name docker default
```

- Запускаем роль:

```
ansible-playbook -i hosts.ini site.yml

```