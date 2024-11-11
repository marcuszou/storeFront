# Setup MySQL Server in Linux

## Completely remove any previous config
```shell
sudo apt remove --purge mysql*
sudo apt autoremove
sudo find / -iname mysql
```
## Install the mysql-server
```shell
sudo apt update
sudo apt install mysql-server
```
## Run the wizard
```shell
sudo mysql_secure_installation
sudo mysql
mysql> use mysql;
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
```
## Enable password login (replace 'password' part)
```shell
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
mysql> FLUSH PRIVILEGES;
mysql> exit;
```
## You should be able to login with password now
```shell
mysql -u root -p
Enter password:

mysql>
```