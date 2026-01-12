Here we are hosting the frontend by using nginx-webserver

installation of nginx

dnf install nginx -y 

Commands used to enable and start nginx

systemctl enable nginx
systemctl start nginx

Try to access the service once over the browser and ensure you get some default content

Remove the default content that web server is serving.

rm -rf /usr/share/nginx/html/*

Download the frontend content

curl -o /tmp/frontend.zip https://expense-joindevops.s3.us-east-1.amazonaws.com/expense-frontend-v2.zip

Extract the frontend content.

cd /usr/share/nginx/html
unzip /tmp/frontend.zip

Try to access the nginx service once more over the browser and ensure you get expense content.

Then create nginx reverse proxy configuration and restart the nginx 

systemctl restart nginx




