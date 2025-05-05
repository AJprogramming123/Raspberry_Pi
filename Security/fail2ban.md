# Fail2ban & IPtable

### 1.) <cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local>:
    [sshd]
    enabled = true
    port = ssh
    Logpath = %(sshd-log)s
    backend = systemd
    maxretry = 3
    findtime = 600
    bantime = 3600

- The way I found out which configuration to pick was through the conf file of fail2ban after installation, it had its own sshd portion which made it easier, not only that this seem to be the only needed step to configure, fail2ban has their own commands automatically to add 'iptables' features to its banned.
- [logpath] This parameter detemines where to look for log entries related to failed login attempts. %(sshd-log)s is a variable in Fail2Ban that refers to the system log file used for SSH attempts.
  - How to Find out the Exact Log file on Your System:
    - <grep sshd /var/log/auth.log>
- [backend] 'systemd' tells fail2ban to not look for tradition log files, only read from the systemd journal directly. systemd is the system and service manager that use systemctl for managing service.

--------------

### 2.) <fail2ban-client status sshd>
- Shows running jails and any banned IPs. This is useful letting me know that its working.
---------------

### 3.) <apt install iptables>
- Manadatory step, when i was attempting to start/emable fail2ban all was missing was the iptables which is used to configure the Linux kernel's built-in firewall.
- set up rules for filtering network traffic based on IP addresses, ports, protocols, and other network-related parameters.
- basics fial2ban has their own built in commands to be able to ban these IP addresses it does it through the iptables.
- 
---------------

### 4.) <fail2ban-client set sshd unbanip <IP_ADDR>>

---------------
# Images
