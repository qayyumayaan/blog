# Raspberry Pi Zero 2W Guide: Controlling the Motors
By Ayaan 3-10-25

This guide goes into the steps needed to enable I2C to be able to control motors from the Raspberry Pi. 

## 1) Pull the files from GitHub

For our project, the files are located on GitHub at this [link](https://github.com/hransom528/ECECapstoneProject). 

Make sure Git is installed.
```bash
sudo apt update
sudo apt install git -y
```

Navigate to the repository you want to clone the files to. Clone the Git repository. Here we will copy it to Desktop. 
```bash
cd ~/Desktop
git clone https://github.com/hransom528/ECECapstoneProject.git
```

## 2) Install Python dependencies

Be sure that Python is installed with:
```bash
sudo apt install python3 python3-venv python3-pip -y
```

Check if Python is installed with:
```bash
python3 --version
```

We can create and then activate a virtual Python environment called `myvenv` to install our dependencies. 

```bash
python3 -m venv myvenv
source myenv/bin/activate
```

You should see a `(myenv)` at the beginning of your terminal. 

Now install the dependencies with: 

```bash
sudo apt update && sudo apt install python3-pip python3-smbus i2c-tools -y
pip3 install adafruit-blinka adafruit-circuitpython-motorkit
```

## 3) Run the code

Navigate to the proper directory:
```bash
cd ECECapstoneProject
```

Now you can run the code! Let's run the `control_movement.py` in the `motor-control` directory: 
```bash
python3 motor-control/control_movement.py
```