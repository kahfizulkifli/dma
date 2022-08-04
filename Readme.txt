sudo adduser --disabled-password --gecos "" kahfi
sudo usermod -aG sudo kahfi
    sudo su 
    cp -r /home/cc/.ssh /home/kahfi
    chmod 700  /home/kahfi/.ssh
    chmod 644  /home/kahfi/.ssh/authorized_keys
    chown kahfi  /home/kahfi/.ssh
    chown kahfi  /home/kahfi/.ssh/authorized_keys
    echo "kahfi ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/90-cloud-init-users
    exit
    exit
  
0. Setup zsh [Login on "kahfi"]

    ssh 129.114.109.30 

        sudo su
        apt-get install zsh -y
        chsh -s /bin/zsh root

        # Break the Copy here ====

        exit
        sudo chsh -s /bin/zsh kahfi
        which zsh
        echo $SHELL

        sudo apt-get install wget git vim zsh -y

        # Break the Copy here ====

        printf 'Y' | sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

        /bin/cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
        sudo sed -i 's|home/kahfi:/bin/bash|home/kahfi:/bin/zsh|g' /etc/passwd
        sudo sed -i 's|ZSH_THEME="robbyrussell"|ZSH_THEME="risto"|g' ~/.zshrc
        zsh
        exit
        exit

1. Setup dir
sudo mkdir -p /mnt/extra
sudo chown kahfi -R /mnt
cd /mnt/extra

2. Update kernel code
sudo apt-get install linux-headers-`uname -r` # this is to install the headers of the linux, so that we can build the kernel code
make all # compile the code with the files from the kernel code
# ther should be many modules created, .ko, .o, .cmd
sudo su # enter root mode
insmod dma-example.ko # insert module of dma-example into kernel
dmesg # check if the module is inserted, the output should look like this
[80739.257789] DMA fifo test start
[80739.257792] queue size: 32
[80739.257793] queue len: 12
[80739.257795] DMA sgl entries: 2
[80739.257796] scatterlist for receive:
[80739.257800] sg[0] -> page 000000002dd990c3 offset 0x00000b2d length 0x00000013
[80739.257803] sg[1] -> page 000000002dd990c3 offset 0x00000b20 length 0x00000001
[80739.257804] DMA sgl entries: 1
[80739.257805] scatterlist for transmit:
[80739.257807] sg[0] -> page 000000002dd990c3 offset 0x00000b21 length 0x00000008
[80739.257808] queue len: 7
[80739.257809] test passed

3. Safety
# Looks like doing floating point in kernel code is risky --> move to user-space

4. DMA-example
https://schaumont.dyn.wpi.edu/ece4530f19/lectures/lecture22-notes.html#direct-memory-access
# ERROR: cannot find system.h