### Nodejs + Express

acme.sh --issue -d nodejs.ouaisheinie.cn -w /root/home/nodeBlog/public

ssl_certificate         /home/ssl/nodejs.ouaisheinie.cn.key.pem;
ssl_certificate_key     /home/ssl/nodejs.ouaisheinie.cn.key;
ssl_dhparam             /home/ssl/nodejs.ouaisheinie.cn.dhparam.pem;


# 增加

acme.sh --installcert -d nodejs.ouaisheinie.cn \
               --keypath       /root/home/ssl/nodejs.ouaisheinie.cn.key  \
               --fullchainpath /root/home/ssl/nodejs.ouaisheinie.cn.key.pem \
               --reloadcmd     "sudo nginx -s reload"

# 生成
openssl dhparam -out /root/home/ssl/dhparam.pem 2048

<!-- 
非https 配置
server {
    listen 80;
    server_name nodejs.ouaisheinie.cn;
    root /root/home/nodeBlog/public;

    try_files $uri/index.html $uri @nodejs;
    location @nodejs {
        proxy_pass http://127.0.0.1:5000;
        proxy_http_version 1.1; 
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
     }
}
 -->