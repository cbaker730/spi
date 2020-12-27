# spi



## Preparation

On host, create two SSH keys - two each with a different passphrase (key_relay, key_admin), one without (key_pi)

    ssh-keygen





## Set up relay server using key_admin.pub. Assign a static IP address and assign to DNS name relay.domain.com

Connect to relay server over SSH using key_admin, change SSH port, and reconnect

    ssh -i /home/kali/.ssh/key_admin kali@relay.domain.com
    sudo apt update && sudo apt upgrade -y
    sudo nano /etc/ssh/sshd_config
      (Add a line for 'Port 2222' and save)
    sudo systemctl restart ssh
    exit
    ssh -i /home/kali/.ssh/key_admin kali@relay.domain.com -p 2222





## Set up RPi

Format RPi with latest Kali ARM

Connect to RPi over SSH, change default password, and make a directory for the keys

    ssh kali@10.10.10.10 (password: kali)
    passwd
      (Change password)
    mkdir -p /home/kali/.ssh
    sudo apt update && sudo apt upgrade -y

Copy key_pi and key_relay.pub to RPi. Rename key_relay.pub -> authorized_keys

    scp key_pi kali@10.10.10.10:/home/kali/.ssh
    scp key_admin.pub kali@10.10.10.10:/home/kali/.ssh/authorized_keys
    
Connect to RPi over SSH using key_admin

    ssh -i /home/kali/.ssh/key_admin kali@10.10.10.10
    
    
    
    
    
    
    

    

TODO:
disable kali account
move ssh to port 2222
