security-config.yml работает с ргуппой new, настраивает сервер с нуля (ssh, firewall)

Логин группы new по паролю

vars:

security-installetion/vars/main.yml

ssh_whitelist: |
  192.168.5.1
  192.168.5.39
  192.168.5.38


rsa ключ копируется на сервер из /root/.ssh/id_rsa.pub

запуск:
ansible-playbook -i hosts security-config.yml

-------------------------------------------------------------------------------------------------------------

install-lnmp.yml работает с группой test (подключение по rsa key) устанавливает nginx php8.1-fpm с модулями, mysql  и делает базовую настройку этих пакетов

vars:

lnmp/vars/main.yml

параметр mysql_root_password задаёт пароль рута mysql

запуск:
ansible-playbook -i hosts install-lnmp.yml

-------------------------------------------------------------------------------------------------------------

wp-deploy.yml работает с группой test (подключение по rsa key) разворачивает проект wp (создает virtual-host, user linux, user db, db, скачивает и разворачивает wp, настраивает wp-config.php)

vars:

wp-deploy/vars/main.yml

DOMAIN_NAME: wp.example.com
user_password: userpass
mysql_root_password: myrootpass
name_db: wp
user_db: wp
password_user_db: userdbpass

запуск

ansible-playbook -i hosts wp-deploy.yml
