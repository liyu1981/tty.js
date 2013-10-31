# 1. make a copy of bash -> rbash

```bash
  cp /bin/bash /opt/rbash
```

# 2. as root add a guest user and setup its home

```bash
  useradd guest -s /opt/rbash
  mkdir -p /home/guest/bin
  mkdir -p /home/guest/.ssh
  touch -p /home/guest/.ssh/known_hosts
  chown guest:guest /home/guest/.ssh/known_hosts
```

# 3. make the ssh client avaliable to him

```bash
  ln -s /usr/bin/ssh /home/guest/bin/ssh
```

# 4. restrict him can only use the cmds in his realm

```bash
  echo 'export PATH=$HOME/bin' > /home/guest/.bashrc
  chmod 755 /home/guest/.bashrc
  chown root:root /home/guest/.bash_rc
  ln -s /home/guest/.bashrc /home/guest/.bash_profile
```

# 5. change gid & uid & home in config.json

make it correct to be guest account

```bash
  id guest
```

# 6. if not work, rebuild dependencies of tty.js 

```bash
  npm rebuild
```

# 7. (optional) setup the nat mapping

```bash
  iptables -A OUTPUT -o eth1 -m owner --uid-owner 1002  -j DROP
```
