## LKS Jateng 2023 


### Install Node.Js & Depedency

```
sudo apt update
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo npm install bootstrap
sudo npm add axios
sudo npm install react-router-dom
```

### Clone Repository

```
cd ~
git clone https://github.com/assyafii/product-apps.git
cd product-apps
```


### Install & Running React apps

```
cd product-apps
npm install 
npm run build 
npm start 
```


### Setup React Apps running on backend

#### Create systemd

```
sudo nano /lib/systemd/system/product.service
```

Add code bellow :

```
[Unit]
After=network.target
 
[Service]
Type=simple
User=root
WorkingDirectory=/home/ubuntu/product-apps
ExecStart=/usr/bin/npm start 
Restart=on-failure
 
[Install]
WantedBy=multi-user.target

```

#### Restart services

```
sudo systemctl daemon-reload
sudo systemctl start product
sudo systemctl enable product
sudo systemctl status product
```

### Install Nginx
```
sudo apt update
sudo apt-get install nginx
```

### Setup nginx for reverse proxy


```
sudo nano /etc/nginx/sites-available/product-apps.conf

server {
    listen 80;
    location / {
        proxy_pass http://localhost:3000;
    }
}
```

```
sudo unlink /etc/nginx/sites-enabled/default
sudo ln -s /etc/nginx/sites-available/product-apps.conf /etc/nginx/sites-enabled/product-apps.conf
sudo systemctl restart nginx
sudo systemctl status nginx
```



Semangat yaa :)
