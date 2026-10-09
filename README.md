1) Запустить на ВМ как systemd сервис приложение на python
 ```
[Unit]
Description= app_py
After=network-online.target

[Service]
User=matvey
Group=matvey
WorkingDirectory=/var/www/static
ExecStart=/var/www/static/venv/bin/gunicorn --bind 127.0.0.1:8001 app:app
Restart=Always

[Install]
WantedBy=multi-user.target
```


2)Создать директорию /var/www/static, в ней создать файлы index.html, style.js и Скачать лого nginx

![](https://github.com/matveyframe/Lesson_14/blob/main/landing-status_result.PNG "Logo Title Text 1")

3)Настроить Nginx в качестве прокси для созданного в пп1,2 приложения
<p>-nginx проксирует запросы на flask-бэкенд </p>
<p>-nginx раздает статические файлы из директории /var/www/static </p>

app_proxy:
```
server {
listen 8000;
server_name localhost;

 access_log /var/log/nginx/app_access.log;
 error_log /var/log/nginx/app_error.log;

location /static/ {

        alias /var/www/static/;
}

location / {

        proxy_pass http://127.0.0.1:8001;

}
   }
```
Main Page:
![](https://github.com/matveyframe/Lesson_15/blob/main/Result%20main%20page.PNG "Logo Title Text 1")
API:
![](https://github.com/matveyframe/Lesson_15/blob/main/Result%20API.PNG "Logo Title Text 1")
Response:
![](https://github.com/matveyframe/Lesson_15/blob/main/Result%20response.PNG "Logo Title Text 1")
Index:
![](https://github.com/matveyframe/Lesson_15/blob/main/Result%20index.PNG "Logo Title Text 1")
