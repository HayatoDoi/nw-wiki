# nw-wiki Docs

## To run

### docker
```bash
$ docker-compose up
```
Open `http://127.0.0.1:4000` in your browser

### native
```bash
$ apt install python3 python3-dev jpeg-dev
$ pip3 install --upgrade pip
$ pip3 install blockdiag nwdiag

$ bundle install
```

## How to use 404 page
### nginx
```
error_page 404 /<base_url>/404.html;
```

### apache
Enable .htaccess
