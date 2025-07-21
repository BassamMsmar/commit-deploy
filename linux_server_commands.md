# restart server
reboot

## update packages
sudo apt update
sudo apt upgrade

## install packages
sudo apt install <package_name>

## remove packages
sudo apt remove <package_name>

## remove packages and config
sudo apt purge <package_name>

## remove packages and config and dependencies
sudo apt autoremove

## remove packages and config and dependencies and cache
sudo apt clean

## run script
chmod +x deploy.sh
./deploy.sh


# remobe puplic keys
ssh-keygen -R 185.213.27.212



