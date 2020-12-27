# spi



Format RPi with latest Kali ARM

Connect to RPi over SSH, change default password, and make a directory for the keys

    ssh kali@10.10.10.10 (password: kali)
    passwd
    mkdir -p /home/kali/.ssh

On host, create two SSH keys - two each with a different passphrase (key_relay, key_admin), one without (key_pi)

    ssh-keygen

Copy key_pi and key_relay.pub to RPi. Rename key_relay.pub -> authorized_keys

    scp key_pi kali@10.10.10.10:/home/kali/.ssh
    scp key_admin.pub kali@10.10.10.10:/home/kali/.ssh/authorized_keys
    
Connect to RPi over SSH using key_admin

    ssh -i /home/kali/.ssh/key_admin kali@10.10.10.10
    

    
