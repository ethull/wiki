# quick fix
    grub -> e -> add nomodeset to linux line as a param
    //once logged on
        sudo vim /etc/default/grub
            GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"

//TODO add nvidia primus solution instructions
# nvidia prime
## setup
    //install packages, possbility may need a different nvidia driver
        sudo apt install nvidia-390 nvidia-prime

    //if you want vulkan support need the latest driver (may be buggy)
        sudo add-apt-repositary ppa:graphics-drivers/ppa
        sudo apt update
        sudo apt install nvidia-driver-430
## use
    //switches active GPU on next boot
        sudo prime-select nvidia

## remove
    //if need to swap nvidia driver 
        sudo apt remove nvidia-*
        //reboot before installing next one
