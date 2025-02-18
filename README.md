# ToDoList WebApp

This is a Django-based web application for managing a to-do list. Follow the instructions below to set up and run the project on your computer.
Recommend using Ubuntu

## Prerequisites

- Python 3.12 or higher
- PostgreSQL
- Node.js
  - Ensure that you have add Node .js into PATH
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

##### <span style="color:red">PLEASE MAKE SURE THAT YOU DO NOT SKIP THIS STEP AND DO SIMILARLY TO THIS INSTRUCTION!</span>
 
First, after finishing install PostgreSQL, need to create PostgreSQL user and database for this project. 
We run PostgreSQL by this command:

```sh
sudo -u postgres psql
```
- In the PostgreSQL prompt, run the following commands to create PostgreSQL user and database for this project:

```sh
CREATE USER todo_user WITH PASSWORD 'mypassword';
CREATE DATABASE todo_db OWNER todo_user;
ALTER USER todo_user CREATEDB;
\q 
```
2. Update settings.py:

- After creating PostgreSQL user and database for this project, open your setting.py file in .\Backend\todo_backend\setting.py
- Do not change anything in this file here and just CHECK the DATABASES configuration in settings.py is correct as below:

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

Next, run these command lines:

```sh
python Backend/manage.py makemigrations
python Backend/manage.py migrate
```

Finish! You have successfully set up database for this project. Now let run the server and the frontend in next step

### 5. Run the Development Server

Please make sure that you are standing at Backend folder .\Backend, and run the following command to run the server:

```sh
python manage.py runserver
```

Next, simutanously, make sure that you are at .\Frontend\todo_frontend, and run this code:

```sh
npm install
npm start
```

## FINISHED~~

You will see the new window open by browser, this is our project!


