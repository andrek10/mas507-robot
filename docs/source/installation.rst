###################
Jetbot installation
###################

This section will go through all necessary steps to install software on Jetson Nano for MAS507.
There are two major steps involved:

1. Reformatting the SD card with a Linux-based operating system
2. Setup communication
3. Installing necessary software

The teacher should make sure that step 1 is already performed before starting the project, and the students should only perform step 2 and 3.

***************************
Installing operating system
***************************

This step requires a monitor with HDMI or displayport, a keyboard and a moouse.
The steps are as follows:

- Follow the instructions `here <https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write>`_ for writing the ISO file to the SD card.
- Put SD card back into Jetson
- Connect monitor, mouse and keyboard to Jetson
- Connect ethernet cable for updates (optional)
- Connect power to Jetson
- Once booted, the installation process can proceed

During the installation, these options should be made:

- User name: jetbot
- Password: jetbot
- Computer name: mas507-jetbot-<group-number>
    - For example, for group 3 (box with 3 on): mas507-jetbot-3

After installation, you can update the system with

.. code-block:: console

    sudo apt update && sudo apt -y upgrade

After update, the ethernet port is set to static IP for communication with any laptop.
Click network icon in status bar upper left corner.
Should look like two arrows when only ethernet is connected.
On the bottom of the list, choose "Edit Connections..."
Double click on the wired connection profile that exists.
Click on "IPv4 Settings" tab.
Set method to "Manual" and add a new address:

- Address: 192.168.0.3
- Netmask: 255.255.255.0
- Gateway: blank

Click on "Routes" button in lower right corner.
Activate the "Use this connection only for resources on its network".
This will make sure that Ubuntu only uses LAN for local connections, and will not try to use it for internet access over WiFi.
Click OK, Save etc. 

You should now reboot the Jetson to allow for updates to be installed. 

*******************
Setup communication
*******************

There are two main ways of communicating with the Jetbot for programming it:

1. Terminal/SSH
2. Remote desktop environment

The second choice of remote desktop environment is recommended for most of the programming tasks in this project.
However, the setup of this environment requires some configuration over SSH.
First, the windows computer should be set to a fixed IP address.

Fixed IP Windows
================

Open Network settings on Windows computer and set static IP address to **192.168.0.1**, and mask **255.255.255.0**.
Generally if you have an ethernet port, the following procedure should work:

- Open Settings/cogwheel in start menu
- "Network and Internet" tab
- Change adapter options
- Find Ethernet adapter
    - Double click
- Enter properties
- Scroll down to "Internet Protocol Version 4 (TCP/IPv4)"
    - Double click
- Set static IP address

.. figure:: ./figs/ssh/staticIP.*

Terminal/SSH
============

The Linux operating system can be used and operated using only a **terminal** (text input and output).
You can update system files, edit files directly in terminal, and run code.

SSH is an abbreviation for "Secure SHell" and allows for opening such a terminal session on a remote host.
This means you can use a Windows computer to operate a Linux system using text input.

To connect to Jetbot using ethernet cable, first connect cable between Jetbot and Windows computer.

MobaXTerm
---------

For SSH on Windows I recommend to install MobaXTerm as it includes an X server for opening Linux windows inside Windows environment.
`MobaXTerm download <https://mobaxterm.mobatek.net/download.html>`_.

- Click Sessions --> New session on the manubar.
- Choose SSH on the top
- Set Remote host: 192.168.0.3 
    
    - Username: jetbot

- Click OK.

This session can be re-opened in the left pane when restarting MobaXTerm.

To paste commands into MobaXTerm, you can either press F12, or you can change the shortcut to CTRL + V:

- Open settings --> Keyboard shortcuts on the menubar.
- Find "Paste in terminal" and replace edit the command to suitable value (for example CTRL + V).

Private and public key
======================

`Guide <https://www.smarthomebeginner.com/connecting-to-ubuntu-server-using-ssh-and-putty/>`_'.

`Microsoft guide <https://code.visualstudio.com/docs/remote/troubleshooting#_configuring-key-based-authentication>`_.

Follow this guide on the Jetson Nano (Either via SSH or screen/mouse/keyboard). 
Copy **one** line at a time:

.. code-block:: console

    cd ~/.ssh
    ssh-keygen -t rsa
    touch authorized_keys
    chmod 600 authorized_keys
    cat id_rsa.pub >> authorized_keys
    rm id_rsa.pub

Move id_rsa to Windows computer. Use this file when configurating for a private key.

Internet on Jetson
==================

The Jetson will get internet from a Windows computer by sharing it over WiFi.
This is possible on most modern Windows computers.

1. Open "Network and Internet" in Settings, and enter "Mobile hotspot"
2. Set the hotspot to share Wifi over Wifi
3. Click Edit and set a suitable network name and password.
4. Click to share connection.
5. Open an SSH terminal on Jetson and enter the command:

.. code-block:: console

    sudo nm-connection-editor

This will bring up a graphical user interface for connections.

6. Click the + icon in lower left corner and choose Wi-FI
7. Under "Wi-Fi" tab, set the SSID to the network name made under hotspot configuration.

    - Also set the connection name to "Windows hotspot"
    
8. Under "Wi-Fi Security", enter the password set under hotspot configuration.
9. Click save and exit the window
10. Activate the connection. Enter in terminal:

.. code-block:: console

    sudo nmtui

11. Go down to "Activate connection" and press enter
12. Use arrow keys and navigate to "Windows hotspot".

    - Press enter. 
    - If selection moves to top of list, navigate to "Windows hotspot" again and press enter.
    - There should be a "Connecting..." box that appears.
    - If successful, there is a star next to "Windows hotspot"

13. Press escape twice to exit

Back in the "Mobile hotspot" panel in Windows, the list of devices connected should say IP address of connected Jetson.

.. figure:: ./figs/wifi/WifiConnection.*

Remote desktop environment
==========================

The Jetbot can be programmed via a remote desktop environment rather than a terminal over SSH.
We have chosen to land on X2Go for the remote access, as it has been stable, and allows for re-connecting to sessions if disconnecting.

Linux part
----------

Install the following software over SSH (**ONE** line at a time):

.. code-block:: console

    sudo apt install -y nano software-properties-common
    sudo add-apt-repository ppa:x2go/stable
    sudo apt update
    sudo apt install -y x2goserver x2goserver-xsession
    sudo apt install -y ubuntu-mate-desktop

Afer installation, reboot the jetbot

.. code-block:: console

    sudo apt reboot

Windows part
------------

On the Windows computer, install `X2Go client <http://code.x2go.org/releases/X2GoClient_latest_mswin32-setup.exe>`_.
Install with recommended components.
Once X2Go client is opened, make a new session by clicking "Session" --> "New session" at the top bar.
Lets first make an ethernet session

- Session name: Ethernet Jetson
- Host: 192.168.0.3
- Login: jetbot
- Session type: MATE
- Keep rest as default. 

.. figure:: ./figs/x2go/jetsonEthernet.*

Under "Media" tab, disable sound support. 
To improve connection, you may also change settings under "Connection" and "Input/Output" tab to your liking.
For cabled ethernet, the default "Connection" settings are usually OK. 
Click OK. 
The session should be available on the right-hand side. 
Click it and enter password "jetbot", and OK. 
It should connect to Jetbot over Ethernet and a desktop environment should be visible. 
Programs are visible in the Menu in the top-left corner.

Remember that closing the remote desktop windows does **not** log out of the session on Jetbot.
If you re-connect after closing the window, the desktop environment should be back where you left of.
In order to completely log out, you should click the menu button, and choose to log out. 

*****************************
Installing necessary software
*****************************

Open a terminal in the remote desktop environment.
In this session, we will install software for use in Python and others.

Lets start with system tools (Copy **one** line at a time):

.. code-block:: console

    sudo apt install -y python3-pip libi2c-dev i2c-tools python3-pil

Python packages (Copy **one** line at a time):

.. code-block:: console

    pip3 install numpy
    pip3 install Jetson.GPIO
    pip3 install Adafruit_PCA9685
    pip3 install adafruit-circuitpython-ssd1306

IDLE X
======

Installation
------------

IDLE is a Python development interface.
IDLE X is IDLE with extra extensions (like line numbers).
To install, open a terminal in the remote desktop:

- Go to downloads folder by typing:

.. code-block:: console

    cd /home/jetbot/Downloads

- Download a zip fil with IDLEX using

.. code-block:: console

    wget http://sourceforge.net/projects/idlex/files/idlex-1.18.zip/download

- Unzip file with

.. code-block:: console

    unzip download

- Open the folder and install IDLEX

.. code-block:: console

    cd idlex-1.18
    python3 setup.py install --user

- Now, IDLE X can be started with: (The ending & means that it starts in a new process, and keeps the terminal open for other input)

.. code-block:: console

   idlex & 

Using IDLE X
------------

IDLE X opens with a Python console which accepts user input.
The "File" menubar lets you make new Python files, or edit old ones.
Python files can be run using F5 button.

GPIO
====

GPIO are general purpose IO pins, which are the 40 pins on the Jetson.
We need access to them for communicating with motor driver etc.
By default, only root user can access them, but it should be opened by the normal jetbot user. 
Follow these instructions (as based on `JetsonHacks <https://www.jetsonhacks.com/2019/06/07/jetson-nano-gpio/>`_):

Add "jetbot" user to list for accessing GPIO devices. 

.. code-block:: console

    sudo groupadd -f -r gpio && sudo usermod -a -G gpio jetbot

Copy custom rules to another folder

.. code-block:: console

    sudo cp /opt/nvidia/jetson-gpio/etc/99-gpio.rules /etc/udev/rules.d/

Reload rules:

.. code-block:: console

    sudo udevadm control --reload-rules && sudo udevadm trigger

Add jetbot user to i2c group for permission

.. code-block:: console

    sudo adduser jetbot i2c

Reboot for the changes to be in effect.


