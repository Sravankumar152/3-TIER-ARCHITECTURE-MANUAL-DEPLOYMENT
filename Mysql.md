Steps to configure Db Server:

Here we are using mysql server 8.0.x 

Install mysql

dnf install mysql-server -y

Start mysql service

systemctl enable mysqld
systemctl start mysqld

Next, We need to change the default root password in order to start using the database service. 

mysql_secure_installation --set-root-pass ExpenseApp@1

verification:

We can check data by using client package called mysql.

Usually command to connect mysql server is
mysql -h <hostaddress> -u root -p<password>


use the netstat -lntp to check the port db default port is 3306