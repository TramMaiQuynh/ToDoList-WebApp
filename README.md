# ToDoList WebApp

This is a Django-based web application for managing a to-do list. Follow the instructions below to set up and run the project on your computer.

## Prerequisites

- Python 3.12 or higher
- PostgreSQL
- Virtualenv </br>
  - Ensure that the virtual environment is activated whenever you work on the project.

## Setup Instructions

Please make sure that follow ALL instructions below

### 1. Clone the Repository

```sh
git clone https://github.com/TramMaiQuynh/ToDoList-WebApp

cd ToDoList-WebApp
```


### 2. Create and Activate Virtual Environment

```sh
python -m venv todoenv
source todoenv/bin/activate
```

### 3. Install Dependencies

```sh
pip install -r requirements.txt
```

### 4. Configure PostgreSQL

0. Make sure that you have already installed PostgreSQL. If not, please install first.

- Ubuntu:

Before installing PostgreSQL, update the system's package list:

```sh
sudo apt update && sudo apt upgrade -y
```

Next, install PostgreSQL

```sh
sudo apt install postgresql postgresql-contrib -y
```
After installing, start and enable the PostgreSQL service:

```sh
sudo systemctl start postgresql
sudo systemctl enable postgresql
```
Next, Check the service status:

```sh
sudo systemctl status postgresql
```
Last, check the database connection by switching to the PostgreSQL user and enter the database shell:

```sh
sudo -i -u postgres
psql
```
If it works without errors, your installation is SUCCESSFUL. Exit with:

```sh
\q
exit
```

- Windows:

Go to this link: https://www.enterprisedb.com/downloads/postgres-postgresql-downloads and download the .exe file suitable to your system


1. Create a PostgreSQL user and database:

```sh
sudo -u postgres psql
```
- In the PostgreSQL prompt, run the following commands:

```sh
CREATE USER todo_user WITH PASSWORD 'mypassword';
CREATE DATABASE todo_db OWNER todo_user;
ALTER USER todo_user CREATEDB;
\q 
```
2. Update settings.py:

- Ensure the DATABASES configuration in settings.py is correct:

```sh
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'todo_db',
        'USER': 'todo_user',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '5432',
    },
    'test': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'test_todolist',
        'USER': 'todo_user',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}

if 'test' in sys.argv:
    DATABASES['default'] = DATABASES['test']

```

5. Apply Migrations

```sh
python Backend/manage.py makemigrations
python Backend/manage.py migrate
```

6. Run the Development Server

```sh
python Backend/manage.py runserver
```


