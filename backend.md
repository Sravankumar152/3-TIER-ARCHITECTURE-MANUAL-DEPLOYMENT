Backend service is responsible for adding the given values to database. Backend service is written in NodeJS, Hence we need to install NodeJS 20.

You can list modules by using dnf module list

dnf module disable nodejs -y
dnf module enable nodejs:20 -y
dnf install nodejs -y

after the installation of nodejs update the openssl packages

dnf update -y openssh openssh-server openssh-clients

Application configuration

Create a Application user (service account)

useradd expense

User expense is a function / daemon user to run the application. Apart from that we don't use this user to login to server.

Also, username expense has been picked because it more suits to our project name.

We keep application in one standard location. This is a usual practice that runs in the organization.

Setup app directory

mkdir /app

Download the application code to create app directory

curl -o /tmp/backend.zip https://expense-joindevops.s3.us-east-1.amazonaws.com/expense-backend-v2.zip

the zip file is going to store in /tmp directory

cd /app

unzip the zip file in /app by using this command

unzip /tmp/backend.zip

These node js application has some dependencies 

Let's download dependencies

cd /app

npm install

then we need to setup a new .service in systemmd so systemctl can manage the service

Setup SystemD Expense Backend Service

vim /etc/systemd/system/backend.service

[Unit]
Description = Backend Service

[Service]
User=expense
Environment=DB_HOST="172.31.24.206"
ExecStart=/bin/node /app/index.js
SyslogIdentifier=backend

[Install]
WantedBy=multi-user.target

After the configuration reload the demon servie

systemctl daemon-reload

Installing mysql client for application server:

dnf install mysql -y

Load schema by connecting to database from the application server

mysql -h 172.31.24.206 -uroot -pExpenseApp@1 < /app/schema/backend.sql

Check in the db server after this configuration whether the Db schema is loaded or not

you can able to see the transaction db and tables

after this configuration start the backend servcie by using 

systemctl enable backend
systemctl start backend

use netstat -lntp to check the ports
