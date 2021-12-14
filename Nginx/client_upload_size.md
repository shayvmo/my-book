### 修改上传大小限制



在配置文件 `  server ` 块下的 ` servername ` 下，增加 ` client_max_body_size 10M; ` 即可。

大小根据需要调整即可。

保存后，重新载入配置 ` nginx -s reload ` 。

例如：

```
server {
    listen       80;
    server_name  shayvmo.test;
    client_max_body_size 10M;
    root   /www/shayvmo/laravel-backend/public;
    index  index.html index.php  index.htm;
    #charset koi8-r;
    location / {
        try_files $uri $uri/ /index.php$is_args$query_string;
    }

    # 以下省略...
}
```

