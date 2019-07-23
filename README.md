# test
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

#		#open terminal
#	mkdir -p $xYOCTO_LOC
#	cd $xYOCTO_LOC
#	git clone -b $xYOCTO_VER git://git.yoctoproject.org/poky.git $xYOCTO_VER &
#
#	cd $xYOCTO_LOC/$xYOCTO_VER
#	git clone -b $xYOCTO_VER git://git.openembedded.org/meta-openembedded  &
#	git clone -b rel-$xVIVA_VER https://github.com/Xilinx/meta-xilinx.git  &
#	git clone -b rel-$xVIVA_VER http://github.com/Xilinx/meta-petalinux  &
#	git clone -b rel-$xVIVA_VER https://github.com/Xilinx/meta-xilinx-tools.git  &


	#	Make prj-dir &
mkdir -p $xPRJ_LOC
mkdir -p $xPRJ_LOC/build
mkdir -p $xPRJ_LOC/deploy
mkdir -p $xPRJ_LOC/external
mkdir -p $xPRJ_LOC/fpga
mkdir -p $xPRJ_LOC/tmp_fpga
mkdir -p $xPRJ_LOC/doc

#	#	Clone xilinx github
#cd $xPRJ_LOC/external
#git clone https://github.com/Xilinx/u-boot-xlnx.git && \
#git clone https://github.com/Xilinx/device-tree-xlnx.git && \
#git clone https://github.com/Xilinx/arm-trusted-firmware.git && \
#git clone https://github.com/Xilinx/linux-xlnx.git
#
#cd $xPRJ_LOC/external/arm-trusted-firmware
#git checkout xilinx-$xVIVA_VER
#git checkout -b xilinx-$xVIVA_VER-b
#
#cd $xPRJ_LOC/external/device-tree-xlnx
#git checkout xilinx-$xVIVA_VER
#git checkout -b xilinx-$xVIVA_VER-b
#
#cd $xPRJ_LOC/external/u-boot-xlnx
#git checkout xilinx-$xVIVA_VER
#git checkout -b xilinx-$xVIVA_VER-b
#
#cd $xPRJ_LOC/external/linux-xlnx
#git checkout xilinx-$xVIVA_VER
#git checkout -b xilinx-$xVIVA_VER-b


xEnv 2018.3

conda activate py27_env
export xYOCTO_LOC=$HOME/xYocto
export xYOCTO_VER=rocko
export xVIVA_VER=v2018.3
export xPRJ_NAME=JKI_jts250f
export xPRJ_LOC=$HOME/iWork/$xPRJ_NAME

conda activate py27_env
source $xYOCTO_LOC/$xYOCTO_VER/oe-init-build-env $xPRJ_LOC/build
cd $xPRJ_LOC/build

bitbake -s > list

touch .gitignore
echo "*.log" > .gitignore
echo "cache/*" >> .gitignore
echo "tmp/*" >> .gitignore

git init
git add *
git commit -a -m  "initial commit"



## yocto meld로 3자 비교
conf 복사 수정
	bblayers.conf
		YOCTODIR  = "/home/f22/xYocto/rocko"
		DOWNPATH  = "/home/f22/xYocto/rocko_downpath"
		TMPDIR    = "/home/f22/xYocto/rocko_tmp/cube-jtf250f"
	sanity_info
		TMPDIR     /home/f22/xYocto/rocko_tmp/cube-jtf250f
		SSTATE_DIR /home/f22/xYocto/rocko_tmp/cube-jtf250f/sstate
meta-infocube 복사

script 복사

src 복사
 cube-zynqmp/cube-${MACHINE-NAME}
 cube-zynqmp/cube-jtf250f
	이곳에 psu_init_gpl은 vivado sdk에서 빼서 넣어놔야 한다.







conda activate py27_env
export xYOCTO_LOC=$HOME/xYocto
export xYOCTO_VER=rocko
export xVIVA_VER=v2018.3
export xPRJ_NAME=JKI_jts250f
export xPRJ_LOC=$HOME/iWork/$xPRJ_NAME

source $xYOCTO_LOC/$xYOCTO_VER/oe-init-build-env $xPRJ_LOC/build
cd $xPRJ_LOC/build/script

make yoc_env
	---------------------------------------------
	check yocto env
	yoc TMP   ==> /home/f22/xYocto/rocko_tmp/cube-jts250f
	BBPATH    ==> /home/f22/iWork/JKI_jts250f/build
	DIR_BUILD ==> /home/f22/iWork/JKI_jts250f/build
	PLAT_DST  ==> /home/f22/xYocto/rocko
	MYBOARD   ==> cube-jts250f
	---------------------------------------------


/home/f22/iWork/JKI_jts250f/build/src/linux-xlnx   <= 수정된 커널 소스를 폴더와 함께 복사
/home/f22/iWork/JKI_jts250f/build/src/u-boot-xlnx  <= 수정된 부트로더 소스를 폴더와 함께 복사


source $xYOCTO_LOC/$xYOCTO_VER/oe-init-build-env $xPRJ_LOC/build
cd $xPRJ_LOC/build/script
touch /home/f22/xYocto/rocko/meta-xilinx/meta-xilinx-bsp/recipes-bsp/platform-init/platform-init/cube-zynqmp/cube-jts250f


make yoc_1check
	board     ==> cube-jts250f

	에러나면 아래 파일 추가한다... "oe-init-build-env" 이것을 실행하면 cube-jts250파일이 지워진다.
	mkdir -p /home/f22/xYocto/rocko/meta-xilinx/meta-xilinx-bsp/recipes-bsp/platform-init/platform-init/cube-zynqmp
	touch /home/f22/xYocto/rocko/meta-xilinx/meta-xilinx-bsp/recipes-bsp/platform-init/platform-init/cube-zynqmp/cube-jts250f


make yoc_1uboot

	아래 에러는 rocko와 bb간에 버전이 맞지 않아 그런다 2018.2는 다 지운다.
		ERROR: No recipes available for:
		/home/f22/iWork/JKI_jts250f/build/meta-infocube/recipes-bsp/u-boot/u-boot-xlnx_2018.2.bbappend
		/home/f22/iWork/JKI_jts250f/build/meta-infocube/recipes-kernel/linux/linux-xlnx_2018.2.bbappend

	uboot src_rev가 2018.2만 되고 2018.3은 안된다.


make yoc_1kernel


make yoc_1rootfs



rootfile system에 설치 가능한 list는 /build/list에 있다.



########################################
opkg package nfs 설치
########################################
#   Host에서
sudo apt-get install nginx
sudo gedit /etc/nginx/sites-available/opkg-server
server {
	autoindex on;
	listen 8920 default_server;
	listen [::]:8920 default_server;
	#server_name _;
	root /home/f22/xYocto/rocko_tmp/cube-jts250f/deploy/ipk;
	#location /icoms/ {
	# root /home/ykoh/yocto/tmp_icom/deploy/ipk;
	# try_files $uri $uri/ =404;
	#}
}

sudo rm /etc/nginx/sites-enabled/default
sudo ln -s -f /etc/nginx/sites-available/opkg-server /etc/nginx/sites-enabled/opkg-server
sudo /etc/init.d/nginx restart

#   target에서
host pc에 8920 포트도 반드시 열어준다.
/etc/opkg/opkg.conf 파일에 아래와 같이 추가한다.

src/gz all         http://10.0.0.99:8920/all
src/gz aarch64     http://10.0.0.99:8920/aarch64
src/gz cube_zynqmp http://10.0.0.99:8920/cube_zynqmp

echo "src/gz all         http://10.0.0.99:8920/all" >> /etc/opkg/opkg.conf
echo "src/gz aarch64     http://10.0.0.99:8920/aarch64" >> /etc/opkg/opkg.conf
echo "src/gz cube_zynqmp http://10.0.0.99:8920/cube_zynqmp" >> /etc/opkg/opkg.conf


>> host에서
bitbake -s > list
cat list  | grep pack
bitbake packagegroup-core-nfs
bitbake package-index


>> target에서
opkg update
		Downloading http://10.0.0.99:8920/all/Packages.gz.
		Updated source 'all'.
		Downloading http://10.0.0.99:8920/aarch64/Packages.gz.
		Updated source 'aarch64'.
		Downloading http://10.0.0.99:8920/cube_zynqmp/Packages.gz.
		Updated source 'cube_zynqmp'.
opkg list |grep nfs

opkg install packagegroup-core-nfs-client



ping 10.0.0.100



root
ifconfig eth0 10.0.0.100
mkdir /mnt_nfs
mount -t nfs -o nolock 10.0.0.99:/xMnt/nfs /mnt_nfs
cd /mnt_nfs/jki/pynq




## host에서   ##
bitbake python3-setuptools
bitbake package-index

## target에서 ##
opkg install python3-setuptools
opkg install python3-numpy
opkg install python3-asyncio
opkg install python3-cffi
opkg install python3-pycparser
cd /mnt_nfs/jki/pynq/PYNQ
python3 ./setup_cube.py install
cd /
start_pl_server.py &


#########################################
	Command Line OVERLAY
#########################################
echo 0 > /sys/class/fpga_manager/fpga0/flags
mkdir -p /lib/firmware
cp /mnt_nfs/jki/pynq/system.* /lib/firmware/
echo system.bin > /sys/class/fpga_manager/fpga0/firmware



setenv sdboot_sdrfs 'mmc dev $sdbootdev && mmcinfo; setenv bootargs earlycon clk_ignore_unused root=/dev/mmcblk1p2 rw rootwait rootfstype=ext4 &&load mmc $sdbootdev:$partid 0x30000000 image.ub && gtx_freq 2 26000000 && gtx_freq 3 26000000 && bootm 0x30000000#conf@1'
saveenv

#########################################
	DNS를 올려줘야함
#########################################
iface eth0 inet	static
  address 10.0.0.100
  netmask 255.255.255.0
  network 10.0.0.0
  gateway 10.0.0.1

nameserver 203.248.252.2
nameserver 164.124.101.2


#########################################
	target에 PIP3설치
#########################################
#호스트에서
bitbake python3-pip
bitbake package-index
#타겟에서
opkg install python3-pip


#########################################
		buildessential 설치
#########################################
bitbake packagegroup-core-buildessential
bitbake package-index

opkg install packagegroup-core-buildessential

jupyter-lab --allow-root --no-browser --ip=*
http://127.0.0.1:8888/?token=253bcc95722309f52ce7b6cfe66b16ffcf2ef885b7d94ce7



http://10.0.0.2:8888

pip3 install jupyter_nbextensions_configurator
%config IPCompleter.greedy=True




uio





#########################################
		타겟보드에 DNS 서버 세팅
#########################################
/etc/resolv.conf에 설절된 DNS서버목록이 자동으로 올라오는데, 직접 수정하는것은 아니다.
사용자가 staic으로 지정하기 위해서는 resolvconf를 설치한다.
그리고 아래와 같이 "/etc/network/interface"을 작성한다.
  iface eth0 inet static
     address 10.0.0.100
     netmask 255.255.255.0
     network 10.0.0.0
     broadcast 10.0.0.255
     gateway 10.0.0.1
     dns-nameservers 10.0.0.100 203.248.252.2 164.124.101.2
