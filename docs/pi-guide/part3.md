# Raspberry Pi Guide Part 3/3
By Ayaan 2-24-25
Part 3/3

The goal of this part is to connect to the network and update with all the latest packages on a Pi Zero 2W. 

## 1) Set up a 2 GB memory swap reserve
The goal of this step is to handle the fact that updating requires a lot of RAM which the Pi does not have. This may be optional, but skipping this step has more risks, so I wouldn't recommend it. 

```bash
free -h && \
sudo swapoff -a && \
sudo fallocate -l 2G /swapfile || sudo dd if=/dev/zero of=/swapfile bs=1M count=2048 && \
sudo chmod 600 /swapfile && \
sudo mkswap /swapfile && \
sudo swapon /swapfile && \
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab && \
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf && \
sudo sysctl -p && \
free -h
```

You should see 2 GB of swap memory listed. 

## 2) Connect to WiFi
If you already set your wifi while writing the image to the SD card in Part 1, you may already be connected to the internet. Check with this command: 

```bash
ping 1.1.1.1
```
If it is pinging correctly, your Pi is connected. 

You can also check by checking the IP: 
```bash
ifconfig
```


## 3) Commands to install essential tools and update
This command is going to take a while, so be patient. 
```bash
sudo apt update && sudo apt upgrade && sudo apt install -y aircrack-ng wireshark net-tools nmap
```


## Now you are done!