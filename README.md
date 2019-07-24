
# Install the Python development environment on your system
sudo apt update
sudo apt upgrade
sudo apt install python3-dev python3-pip

# Download && Install anaconda
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
   


# Building the PetaLinux Image 
Set CMA size to be larger, for SDS-alloc buffers.
• for Zynq UltraScale+ MPSoC: Device Drivers -> Generic Driver -> Size in Mega Bytes(1024)     
• for Zynq-7000 SoC: Device Drivers→ Generic Driver option → Size in Mega Bytes(256     
• Enable staging drivers  
-Device Drivers → Staging drivers (ON)     
• Enable APF management drive  
-Device Drivers → Staging drivers → Xilinx APF Accelerator driver (ON)      
• Enable APF DMA drive  
-Device Drivers → Staging drivers → Xilinx APF Accelerator driver → Xilinx APF DMA engines support (ON)      

Note:
For Zynq UltraScale+ MPSoC, you must turn o@ CPU idle and frequency scaling. To do so, mark the
following option
• CPU Power Management → CPU idle → CPU idle PM support (OFF)
• CPU Power Management → CPU Frequency scaling → CPU Frequency scaling (OFF)
• Filesystem Packages -> misc -> gcc-runtime -> libstdc++ (ON)

4. Add device tree fragment for APF driver. 
/project-spec/metauser/recipes-bsp/device-tree/files/system-user.dtsi, add the following
entry:
/{
   xlnk {
       compatible = "xlnx,xlnk-1.0";
   };
};
