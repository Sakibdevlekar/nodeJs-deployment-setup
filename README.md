# nodeJs_Deployment_setup

## 1. Update system
  ```
     sudo apt-get update
  ```

  ```
      sudo apt-get upgrade
  ```

## 2. Check system time and set proper time
- To check time
  ```
     sudo timedatectl
  ```

- To change time zone
  ```
      sudo timedatectl set-timezone Asia/Kolkata
  ```

## 3. Install Node and NPM
```
   sudo curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```

```
   sudo apt install nodejs
```

```
   node --version 
```


## 4. Clone your project from Github

``` 
    sudo git clone <user repo link>
```
## 5. Install pm2 (run app in backgound)
``` 
   sudo npm i pm2 -g
```
``` 
   sudo pm2 start index.js
 ```
``` 
   sudo pm2 startup
```
 - Other pm2 commands
  ```
     pm2 show app
     pm2 status
     pm2 restart app
     pm2 stop app
     pm2 logs (Show log stream)
     pm2 flush (Clear logs)
  ```
  ### - To make sure app starts when reboot pm2 startup ubuntu

## 6. Change security setting for accessing your website 
 ![WhatsApp Image 2023-10-09 at 1 18 04 PM](https://github.com/Sakibdevlekar/nodeJs_Deployment_setup/assets/111329075/f8e0b642-3453-41a2-bb52-37b45017667c)

 

### Then click on **edit inbound rule**  and add some rules
- Add rule and edit port number as per your need
  

![WhatsApp Image 2023-10-09 at 1 24 52 PM](https://github.com/Sakibdevlekar/nodeJs_Deployment_setup/assets/111329075/9e5919e1-d257-4612-be03-fddaf4330a52)


## 7. Install NGINX and configure
  ```
     sudo apt install nginx
  ```
  ``` 
     sudo nano /etc/nginx/conf.d/server.conf
  ```
- Add the following to the location part of the server block
  ```

  server {
    listen 80;
    server_name <here add your domain name>; 

    location / {
        proxy_pass http://127.0.0.1:8000; # here your port number 
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
  }
  ```
  
  ### - Check NGINX config
  ```
     sudo nginx -t
  ```
  
  ### - Restart NGINX
  ```
     sudo systemctl restart nginx
  ```
  
  ### - Check status  of NGINX
  ```
     sudo systemctl status nginx
  ```

## 8. Add SSL with LetsEncrypt
  - Go to this website **[Certboat Instructions](https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal)**
### Just select the operating system  and your server setup in my case Os - Ubuntu20,  Server - Nginx and follow there instructions
