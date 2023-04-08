# Ansible скрипт для балансировки серверов web1 и web2

### В Inventory хранятся конфигурации (web_servers, rrobin)

### VagrantFile нужен, чтобы быстро поднять виртуалки.

### nginx.yml - это playbook для установки ПО (nginx) на сервера. Внутри него (плейбука) 3 роли: balancer, customer, selyavi. 

balancer - собственно сам балансировщик (настраивает балансировщик в round robin);

customer - сервера web1 или web2;

selyavi - отключает selinux и перезагружает сервер.

## Как запустить playbook?

### 1) Для начала следует закинуть в  inventory ipшники хостов с их именами.
### 2) После чего, для удобства просмотра и чтобы заметить изменения веб-страничек нужно в roles/templates/ поменять код шаблона html'a в файлике index.html.j2
### 3) Далее запускаем сам playbook (nginx.yml)
ansible-playbook nginx.yml -  исполняет все tasks файлы всех ролей, которые у нас прописаны.
### 4) В браузере в строке вписываем ipшник balacner'а ставим ":" и после пишем порт 8080.
## Вывод:

![изображение](https://user-images.githubusercontent.com/113580341/230712769-df8e96ed-4743-495a-b337-cc5496b927b5.png)
![изображение](https://user-images.githubusercontent.com/113580341/230712774-e0f9f2eb-5879-4d02-865d-383d369b0541.png)
![изображение](https://user-images.githubusercontent.com/113580341/230712777-ade0751d-e127-460b-b475-2e763ec9b573.png)

#### Лицензия - AMG///// Production

#### Автор: Аведисян В.Г.
