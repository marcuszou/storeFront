# alfonShop - storeFront



## Tech Stack

1. Python: 3.12.7 (download the installer for macOS Sonoma while Ubuntu 24.04 has python 3.12.3)
2. Django: 5.1.3

In case of someones wanting to have Python 3.11 in Ubuntu 24.04, here is the How-to:

```shell
sudo apt update -y
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update -y
sudo apt install python3.11
```

or install python3.11 and pip3.11 by using port in macOS

```
sudo port install python311
sudo port install py311-pip
## The python3 and pip will be installed in /opt/local/bin/

sudo port install mysql8
sudo port install py311-mysqlclient # This is version 2.2.1
```



## Codebase

### 2.3 Django Supported Database Engines
- SQLite  (Intro to this)
- PostgreSQL
- MySQL   (then focus on this)
- MariaDB
- Oracle
- MS SQL Server
### 2.4 Setup the Dev Environment
```shell
## Install venv engine
pip3 install pipenv

## Create a folder
mkdir storeFront
cd storeFront

## create venv while installing django
pipenv install django --python 3.12
## or classic python3 module
## python3 -m venv .venv

## install more modules
pipenv install django-debug-toolbar mysqlclient==2.1.1

## Activate the venv
pipenv shell
## source .venv/bin/activate
```
### 2.5 Create the first Django project
```shell
```

### 4.3 Migration of SQLite
```shell
python manage.py makemigrations
```
<<<<<<< HEAD
### 4.4 migrate
```shell
python manage.py migrate
```
Also install a VScode extension: SQLite (by alexcvzz)

### 4.6 reverting migrations
```shell
python manage.py migrate store 003 ## the last step was 004
```
Then delete related files, that's very tideous!

The best way is to use git -
```shell
git log --oneline
git reset --hard HEAD~1
```
### 4.7 install MySQL
Go to https://dev.mysql.com/downloads/mysql/ to download the MySQL Community Server installer and install it.

In case of WSL, you have to install MySQL in a special way:
1. Open https://dev.mysql.com/downloads/repo/apt/ to download mysql-apt-config_0.8.33-1_all.deb.

2. Run the command below to install and configure the apt repository.
    ```shell
    sudo deb -i mysql-apt-config_0.8.33-1_all.deb
    ```

3. Run commands below to install mysql server:
    ```shell
    sudo apt update
    sudo apt install mysql-server
    ```

4. Run the commands below to tell the status:
    ```shell
    sudo service mysql stop
    sudo service mysql start
    sudo service mysql status
    ```

5. add the PATH into your `.bashrc` file

    ```shell
    export PATH=$PATH:/usr/local/mysql/bin:/usr/local/mysql/lib
    ```
### 4.8 MySQL client tools
- MySQL Workbench (Free)
- TablePlus ($59)
- JetBrains DataGrip ($89 or 30-day trial): we will use this.
    ```shell
    # download linux installer from JetBrains website
    tar -xzvf ~/Downloads/datagrip-2024.2.2.tar.gz
    sudo mv DataGrip-2024.2.2/ /opt/
    /opt/DataGrip-2024.2.2/bin/datagrip
    ## then connect to the mysqld, also execute a query
    CREATE DATABASE storefront
    ```
    Then 
    ```shell
    code .
    ```
    then in the terminal of VS Code, run (have to specify version of mysqlclient):
    ```shell 
    pipenv install mysqlclient==2.1.1
    ```
### 4.9 change the database from sqlite3 to mysql in project's `settings.py` file
```shell
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'storefront',
        'HOST': 'localhost',
        'USER': 'root',
        'PASSWORD': 'Kanada2024!sql'
    }
}
```
Run the Django server. If encountering `NameError: name '_mysql' is not defined`, please add the folllowing to ~/.zshrc file (macOS), or .bashrc fle (Linux).
```shell
export DYLD_LIBRARY_PATH="/usr/local/mysql/lib:$PATH"
```

If the django server is running okay, migrate the new database:
```shell
python manage.py migrate
python manage.py runserver
```
### 4.10 Running Custom SQL
```shell
python3 manage.py makemigrations store --empty
```
then edit the store\migrations\0004_auto_yyyymmdd_hhmm.py file by adding...
```shell
oprations = [
    migrations.RunSQL("""
        INSERT INTO store_collection (title)
        VALUES ('collection1')
        """, """
        DELETE FROM store_collection
        WHERE title ='collection1'
        """)
]
```
then...
```shell
python3 manage.py migrate
```
check the result in DataGrip app.

## License
MIT
