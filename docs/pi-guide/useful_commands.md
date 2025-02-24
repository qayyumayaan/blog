# Useful Commands
The following are some useful commands to use in Kali, Raspbian, and Debian. 
| Command Description                              | Command |
|-------------------------------------------------|---------|
| See IP                                          | `ifconfig` |
| Test WiFi                                       | `ping 1.1.1.1` |
| Run the GUI (works while in SSH)                | `sudo startx &` |
| View Current RAM                                | `free -h` |
| View current files in directory (-h for human readable) | `ls -h` |
| View disk usage                                 | `df -h` |
| Shut the system down                            | `sudo poweroff` |
| Adjust the base config                          | `sudo nano /boot/config.txt` |
| View current resolution                         | `cat /sys/class/graphics/fb0/virtual_size` |
| SSH into the Pi (without USB serial, need IP)   | `ssh kali@IP` |
| Update package lists                            | `sudo apt update` |
| Upgrade installed packages                      | `sudo apt upgrade` |
| Install a package                               | `sudo apt install <package_name>` |
| Remove a package                                | `sudo apt remove <package_name>` |
| View CPU temperature                            | `vcgencmd measure_temp` |
| Check GPU memory usage                          | `vcgencmd get_mem gpu` |
| Check CPU info                                  | `cat /proc/cpuinfo` |
| Check memory info                               | `cat /proc/meminfo` |
| Show running processes                          | `htop` (install with `sudo apt install htop`) |
| Show system resource usage                      | `top` |
| Check disk space usage                          | `du -sh *` |
| Reboot the system                               | `sudo reboot` |
| Edit network config                             | `sudo nano /etc/dhcpcd.conf` |
| Scan for available WiFi networks                | `sudo iwlist wlan0 scan` |
| Connect to a WiFi network manually              | `sudo wpa_supplicant -B -i wlan0 -c <(wpa_passphrase "SSID" "PASSWORD")` |
| Enable VNC                                      | `sudo raspi-config` (navigate to Interface Options) |
| List all USB devices                            | `lsusb` |
| List all PCI devices                            | `lspci` |
| Find system info                                | `uname -a` |
| Find OS version                                 | `cat /etc/os-release` |
| Monitor system logs                             | `tail -f /var/log/syslog` |
| Check startup services                          | `systemctl list-units --type=service` |
| Enable a service to start on boot               | `sudo systemctl enable <service_name>` |
| Disable a service from starting on boot         | `sudo systemctl disable <service_name>` |
| Start a service manually                        | `sudo systemctl start <service_name>` |
| Stop a service manually                         | `sudo systemctl stop <service_name>` |
| Check the status of a service                   | `sudo systemctl status <service_name>` |
| Show IP routing table                           | `ip route show` |
| Show network interfaces                         | `ip addr show` |
| Find Raspberry Pi model info                    | `cat /proc/device-tree/model` |