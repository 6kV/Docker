**create index.html file**

mkdir ~/html
echo "hello world" > ~/html/index.html

**start the nginx docker container**

sudo docker run --name docker-nginx -p 8080:80 -d -v ~/html:/usr/share/nginx/html nginx

**check nginx**
http://localhost:8080/
