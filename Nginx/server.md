# 常用配置

```nginx
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /var/www/html;

	index index.html index.htm index.nginx-debian.html;

	server_name _;

	location / {
		try_files $uri $uri/ =404;
	}

	location /services/ {
		proxy_pass http://backend0:3300/services/;
		proxy_set_header Host $http_host;
		
	}

}
```