# assignment3

## Task 1 and 2
Running the script `setup` will create the `webgen` user and proper directories as well as the `generate_index` script. It will also create the generate-index service and timer files. The service and timer files can be enabled and started by typing:
```
sudo systemctl enable --now generate-index.service
sudo systemctl enable --now generate-index.timer

```
To check that the timer and services are running correctly:
```
sudo systemctl status generate-index.service
sudo systemctl status generate-index.timer
```
To check logs of service or timer:
```
sudo journalctl -u generate-index.service
sudo journalctl -u generate-index.timer
```
## Task 3
### Step 1
Install the nginx package if it already is not installed - ```sudo pacman -S nginx```

To ensure the server runs as the webgen user, modify the `nginx.conf` files by typing:
```
sudo nvim /etc/nginx/nginx.conf
```
and at the top of the file change `#user http;` to `user webgen;`

### Step 2
To create a separate server block file that configures Nginx to serve the index.html file on port 80, modify the `nginx.conf` file to include
```
include /etc/nginx/conf.d/*.conf
```

And to create the directory if it does not exist:
```sudo mkdir -p /etc/nginx/conf.d```

### Step 3
Create the server block file:
```
sudo nvim /etc/nginx/conf.d/webgen.conf
```
For the contents of the file, include: 
```
server {
    listen 80;
    listen [::]:80;
    
    server_name _; #wildcard which means any server_name
    
    root /var/lib/webgen/HTML;
    index index.html;

	location / {
        try_files $uri $uri/ =404;
    }
}
```

Creating a separate server block files allows sites to be disabled easily by just renaming them to add disabled at the end, e.g. `webgen.conf.disabled`. It also makes configurations easier to manage as each configuration has their own separate file.

To check the status of the nginx service you can type:
```
sudo systemctl status nginx
```

To test the nginx configuration:
```
sudo nginx -t
```

