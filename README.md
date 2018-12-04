###手顺

    docker-compose up -d
    mkdir -p /data/cert/letsencrypt/data
    mkdir -p /data/cert/letsencrypt/etc
    mkdir -p /data/cert/letsencrypt/var/lib
    mkdir -p /data/cert/letsencrypt/var/log
    docker run -it --rm -v /data/cert/letsencrypt/etc:/etc/letsencrypt -v /data/cert/letsencrypt/var/lib:/var/lib/letsencrypt -v /data/cert/letsencrypt/var/log:/var/log/letsencrypt -v /data/compose/letsencrypt/letsencrypt-site:/data/letsencrypt certbot/certbot certonly --webroot --register-unsafely-without-email --agree-tos --webroot-path=/data/letsencrypt --staging -d www.shilikaif.com -d wepy.shilikaif.com
    docker run --rm -it --name certbot -v /data/cert/letsencrypt/etc:/etc/letsencrypt -v /data/cert/letsencrypt/var/lib:/var/lib/letsencrypt -v /data/compose/letsencrypt/letsencrypt-site:/data/letsencrypt certbot/certbot --staging certificates
    
    rm -rf /data/cert/letsencrypt
    
    docker run -it --rm -v /data/cert/letsencrypt/etc:/etc/letsencrypt -v /data/cert/letsencrypt/var/lib:/var/lib/letsencrypt -v /data/cert/letsencrypt/var/log:/var/log/letsencrypt -v /data/compose/letsencrypt/letsencrypt-site:/data/letsencrypt certbot/certbot certonly --webroot --email john_04047210@163.com --agree-tos --no-eff-email --webroot-path=/data/letsencrypt --staging -d www.shilikaif.com -d wepy.shilikaif.com
    docker-compose down
    openssl dhparam -out /data/cert/dh-param/dhparam-2048.pem 2048
    crontab -e
    0 0,12 * * * python -c 'import random; import time; time.sleep(random.random() * 3600)' && docker run --rm -it --name certbot -v "/data/cert/letsencrypt/etc:/etc/letsencrypt" -v "/data/cert/letsencrypt/var/lib:/var/lib/letsencrypt" -v "/data/cert/letsencrypt/data:/data/letsencrypt" -v "/data/cert/letsencrypt/var/log:/var/log/letsencrypt" certbot/certbot renew --webroot -w /data/letsencrypt --quiet && docker kill --signal=HUP nginx-proxy
