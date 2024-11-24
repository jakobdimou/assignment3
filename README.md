# assignment3

## Task 1 and 2
Running the script setup will create the `webgen` user and proper directories as well as the `generate_index` script. It will also create the generate-index service and timer files. The service and timer files can be enabled and started by typing 
```
sudo systemctl enable generate-index.service
sudo systemctl start generate-index.service
sudo systemctl enable generate-index.timer
sudo systemctl start generate-index.timer
```

## Task 3 
Install the nginx package if it already is not installed - ```sudo pacman -S nginx```
To ensure the server runs as the webgen user, modify the 
