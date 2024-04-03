# nginx-2420-Philip-

Welcome!

The goal of today is to learn how to go from a fresh Arch Linux server running on DigitalOcean to serving the demo document included below.

<h1> Step 1 </h1>

<h3> Required Components </h3>

in order to be able to make any of the following steps operate properlly, there are a couple of required services that we will ned to download 

#Nginx

To download nginx follow this link and follow along with this link https://www.maketecheasier.com/install-nginx-server-windows/#install-nginx

This will provide the steps to the download process, running nginx, and any troubleshooting you may need to do in case you run into any problems.

<h4> Systemctl </h4>

<h4> Vim </h4>

Since we are already on a fresh Arch Linux server running on DigitalOcean Vim is included to the linux system.

To access, just "Vim" then the file you want to work on 

<h1> Step 2 </h1>

<h3> Serving the demo document <h3>

To create a new directory for your project root you will need to run 

sudo mkdir -p /web/html/nginx-2420

this is where your website documents will be stored.


Next, we'll set up a separate server block for our new server, named "nginx-2420". We'll create a new configuration file for this server block.

sudo vim /etc/nginx/sites-available/nginx-2420

Now, insdie the file we are going to add the following like this. 

server {
    listen 80;
    server_name example.com;
    # example.com will be your actual doman or IP address in the Nginx server block configuration (I used local hub)

    root /web/html/nginx-2420;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

<h1> Step 3 </h1>

<h2> Enabling Server Block </h2>

Create a symbolic link for the server block configuration file to enable it.

sudo ln -s /etc/nginx/sites-available/nginx-2420 /etc/nginx/sites-enabled/

<h1> Step 4 </h1>

<h2> Restarting Nginx </h2>

After making changes to the Nginx configuration, it's essential to restart the service to apply the changes.

sudo systemctl restart nginx


<h1> Step 4 </h1>

You can now create your demo document inside the project root directory /web/html/nginx-2420 and ensure it's accessible via your server's IP address.

<h1> Step 5 </h1>

Visit your server's IP address in your browser to verify that the demo document is being served correctly.


Congratulations! You have successfully set up Nginx to serve a demo document on your Arch Linux server.


 like Vim and Nginx
Nginx configuration, including setting up a separate server block
systemd components, systemctl commands.
