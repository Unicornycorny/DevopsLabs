
## **Ход работы**

1. Инициировать структуру роли “**Docker**” через Ansible-Galaxy
2. Вынести из предыдущего плейбука задачи установки Docker в отдельную роль
3. Параметризовать роль через переменные
4. Создать в gitlab группу для репозиториев с ролями, запушить роль “**Docker**” в репозиторий
5. Создать файл requirements.yml для установки роли Docker из репозитория
6. Запустить приложение на нодах группы [app] используя ansible-playbook с ролью “**Docker**”


Гит для ролей: [Readme](https://gitlab.com/devops9824703/labs.git)

### **Vagrant**
Поднимаем машины

```bash
vagrant up
```

```bash
vagrant status
```
```
Current machine status:

srv1                      running (virtualbox)
srv2                      running (virtualbox)
```

### **Ansible**

#### **Ansible-galaxy**
Прописываем в wsl 
```bash
ansible-galaxy init docker
```
, что создаст базовую структуру для роли docker <br>

После чего создастся директория ```docker``` <br>
Нам необходимо в: 
- *docker/defaults/main.yml* создать переменные.
- *docker/tasks/main.yml* перенести задачи по поднятию докера и использовать вместо значений переменные из *defaults*.

### *Gitlab*

Нужно создать группу в Gitlab -> создать проект с ролью -> запушить туда *docker*

---
### *Ansible*

### *Ansible-galaxy*

- Создаем файл requirements.yml
- Прописываем в нем имя роли, ссылку на репу с ролью, указываем *main* в качестве src.
- в WSL прописываем 
```bash
ansible-galaxy install -r requirements1.yaml
```
```
Starting galaxy role install process
- extracting docker-role to /home/egorp/.ansible/roles/docker-role
- docker-role (main) was installed successfully
```
![alt text](image.png)
![alt text](image-1.png)

- Добавляем роль в *docker-playbook.yml* (roles) и запускаем
```bash
ansible-playbook -i inventory.ini lab2playbook.yml
```

