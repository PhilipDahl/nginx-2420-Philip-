# nginx-2420-Philip-

Welcome!

The goal of today is to learn how to go from a fresh Arch Linux server running on DigitalOcean to serving the demo document included below.

### 1) Ensure your system is all updated
```
sudo pacman -Syu
```

### 2) Installing nginx and enabling.
```
sudo pacman -Sy nginx
sudo systemctl enable nginx
```

### 3) Create a new directory /web/html/nginx-2420
```
mkdir -p web/html/nginx-2420
```

### 4) Make changes to the nginx.config file
```
sudo vim /etc/nginx/sites-available/nginx-2420.conf
#add the following on the HTTP block. This step is important..
include /etc/nginx/sites-enabled/*;
```

### 5) Configuring nginx 
```
sudo vim /etc/nginx/nginx.conf
#run the following command if VIM is unavailable and retry this step.
sudo pacman -Sy vim
```


### 6) when we are inside the file, type/copy-paste the following:
```
server {
    listen 80;
    server_name #your ip address;

    location / {
        root /web/html/nginx-242;
        index index.html;
    }
}
```

## If an error occures, run the following code
```
sudo mkdir -p /etc/nginx/sites-available
sudo mkdir -p /etc/nginx/sites-enabled
```



### 7) Enable the server block and create a symbolic link to sites-enabled directory
sudo ln -s /etc/nginx/sites-available/nginx-2420 /etc/nginx/sites-enabled/

## In this next step, we will configure the html file we have that we created earlier.

### 8) create an index file inside nginx-2420
touch /web/html/nginx-2420/index.html

# NOTE: The root path and the index file name should be the same and exist as the configuration file for nginx.

Vim the index.html file
sudo vim /web/html/nginx-2420/index.html

paste the following

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2420</title>
    <style>
        * {
            color: #db4b4b;
            background: #16161e;
        }
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        h1 {
            text-align: center;
            font-family: sans-serif;
        }
    </style>
</head>
<body>
    <h1>All your base are belong to us</h1>
</body>
</html>
```
#### 7) Were Done! Type in the IP address of your droplet on a browser, and you will see your results.


---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Adding a Firewall

Continuing, the following Tutorial will show how to create a firewall, a backend to place binary systems, a new service files to run the backend, editting server block and adding a proxy to the back end, and testing connection to your backend.

### 1) Always Ensure your systems are up to date.

```
sudo pacman -Syu
```

### 2) Now we need to download UFW to enable the firewall.

Follow the following steps

### 2.1) Download the UFW package

```
sudo pacman -S ufw
```
### 2.2) Enable Service

```
sudo systemctl enable --now ufw.service
```

### 2.3) Deny incoming, Allow outgoing

``` 
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

### 2.4) Allowing IP address to ANY port of 22

```
sudo ufw allow from 164.92.82.77/24 to any port 22
sudo ufw deny from 164.92.82.77
```

### 2.5) Type all of these in your terminal to allow access. 

```
sudo ufw limit ssh 
sudo ufw allow ssh 
sudo ufw allow http
```

### 2.6) Now we will reboot the system to apply the changes. 

```
sudo reboot
```

After that last step your system/droplet shoukd be restarted, now we need to wait for it to reactivate and then sign in again, this will take a while so dont be concernced if you can not log right back in.

Run the following commands once the system is back up. When status verbose is run, you are expected to see a list of ports that are currently connected to the server.

```
sudo ufw enable
sudo ufw status verbose
```

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
