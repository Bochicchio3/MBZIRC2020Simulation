# MBZIRC2020Simulation
Required packages to simulate the Drone


To install:

sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116

sudo apt update

sudo apt-get install ros-melodic-desktop-full ros-melodic-joy ros-melodic-octomap-ros python-wstool python-catkin-tools protobuf-compiler libgoogle-glog-dev

sudo rosdep init

rosdep update

echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc

source ~/.bashrc

sudo apt install python-rosinstall python-rosinstall-generator python-wstool build-essential

sudo apt-get update

sudo apt-get install git

sudo apt-get install gitk git-gui

sudo apt-get update

sudo apt-get install build-essential cmake git libboost-all-dev mercurial libcegui-mk2-dev libopenal-dev libswscale-dev libavformat-dev libavcodec-dev  libltdl3-dev libqwt-dev ruby libusb-1.0-0-dev libbullet-dev libhdf5-dev libgraphviz-dev libgdal-dev

##CLONE ARDUPILOT REPOSITORY
cd ~
git clone https://github.com/ArduPilot/ardupilot
cd ardupilot
git submodule update --init --recursive
Tools/scripts/install-prereqs-ubuntu.sh -y

Reload the path (log-out and log-in to make permanent):

. ~/.profile


INSTALLATE GAZEBO:  http://gazebosim.org/tutorials?tut=install_ubuntu&cat=install
curl -sSL http://get.gazebosim.org | sh
se vi volete male, installatelo compilandelo dal sorgente, ma quello script
ha sempre funzionato in genere.

INSTALLATE ARDUPILOT+SITL:
http://ardupilot.org/dev/docs/setting-up-sitl-on-linux.html
http://ardupilot.org/dev/docs/building-setup-linux.html#building-setup-linux
questi due link installano ardupilot in sè, gia sono molto più utili



>>Add some directories to your search path (Facultative)
vale a dire: aggiungete queste directory al path in cui il vostro pc va a cercare per far partire
le cose;
ATTENZIONE: ONLY if you didn’t run the install-prereqs script from previous step.

Add the following lines to the end of your “.bashrc” in your home directory
(notice the . on the start of that filename. Also, this is a hidden file,
 so if you’re using a file manager, make sure to turn on “show hidden files”).

export PATH=$PATH:$HOME/ardupilot/Tools/autotest
export PATH=/usr/lib/ccache:$PATH

Then reload your PATH by using the “dot” command in a terminal

. ~/.bashrc
(anche solo chiudere e riaprire il terminale, oppure riavviare il pc dovrebbe bastare


-----------------------------------------------------------------------------------
INSTALLATE LE COSE CHE PERMETTONO A GAZEBO DI COMINCARE CON ArduPilot

https://web.archive.org/web/20180503141535/http://ardupilot.org/dev/docs/using-gazebo-simulator-with-sitl.html
ATTENZIONE: questo link è più una reference per avere le fonti, non dovete seguirla passo passo o
vi troverete a disisntallare gazebo e reinstallarlo (male), creando casino con le
dipendenze.


#####ISTRUZIONI PER SCARICARE MODELLI DI GAZEBO#######

Make a gazebo workspace
      cd ~
      mkdir ~/gazebo_ws
      cd ~/gazebo_ws/
      
hg clone https://bitbucket.org/osrf/gazebo_models ~/gazebo_ws/gazebo_models
cd ~/gazebo_ws/gazebo_models
hg checkout zephyr_demos
echo 'export GAZEBO_MODEL_PATH=~/gazebo_ws/gazebo_models' >> ~/.bashrc
source ~/.bashrc


--------------------------------------------------------------------------------
Start the Simulator

In one terminal, enter the ArduCopter directory and start the SITL simulation:

cd ~/ardupilot/ArduCopter
sim_vehicle.py -f gazebo-iris -D --console --map

In another terminal start Gazebo:

cd ~/gazebo
gazebo --verbose worlds/iris_arducopter_demo.world

CREARE UN PACCHETTO GAZEBO-ROS PERSONALIZZATO;
cartella che chiameremo CATKIN WORKSPACE

DA CATKIN WORSKPACE
mkdir src
entrare in src
fare catkin_create_pkg <NOMEPACKAGE>
poi entrare in NOMEPACKAGE
fare le cartelle launch e worlds
e metterci i file di cui a questo link http://gazebosim.org/tutorials?tut=ros_roslaunch&cat=connect_ros
