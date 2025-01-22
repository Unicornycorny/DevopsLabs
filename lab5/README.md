## **Ход работы**

1. Написать Ansible Playbook поднимающий OpenVPN сервер
2. Через Molecule инициировать структуру для роли и вынести задачи поднятия сервера, с конфигурацией через переменные
3. При завершении работы плейбук должен разместить в playbook-dir артефактный ovpn-файл для подключения
4. Роль должна проходить стандартные тестами molecule test
5. Плейбук подключает роль через ansible-galaxy

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