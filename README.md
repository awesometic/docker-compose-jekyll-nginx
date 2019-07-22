## Before run using docker-compose

1. Create Nginx configuration files by executing Nginx once.
```docker
docker run --rm -e PUID=1000 -e PGID=1000 -e TZ=Asia/Seoul --volume /opt/docker/jekyll-nginx:/config -p 8888:80 linuxserver/nginx
```

2. Copy Nginx default server configuration to `config/nginx/site-confs/default`. This makes Nginx as a proxy server that forwards EXTERNAL_PORT to 4000 port of jekyll.

3. Create a new jekyll websites
```docker
docker run --rm --volume "/opt/docker/jekyll-nginx/www:/srv/jekyll" -it jekyll/jekyll jekyll new . -f
```

4. Build that.
```docker
docker run --rm --volume "/opt/docker/jekyll-nginx/www:/srv/jekyll" -it jekyll/jekyll jekyll build
```

5. Then run `docker-compose up -d`

6. If you access to http://server:8888, Nginx server acts as reverse proxy server for Jekyll so that you can see your Jekyll websites.

