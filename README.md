
#	#.Install the Python development environment on your system
#
#sudo apt update
#sudo apt upgrade
#sudo apt install python3-dev python3-pip
#

#. Download && Install anaconda
./Anaconda3-2019.03-Linux-x86_64.sh -u -t
conda create -y -n py27_env python=2.7
conda activate py27_env
conda deactivate




# Setup Yocto R & VIVA2018.3
xEnv 2018.3
conda activate py27_env
export xYOCTO_LOC=$HOME/xYocto
export xYOCTO_VER=rocko
export xVIVA_VER=v2018.3
export xPRJ_NAME=JKI_jts250f
export xPRJ_LOC=$HOME/iWork/$xPRJ_NAME
