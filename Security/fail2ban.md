# Fail2ban & IPtable

### 1.) cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local:
    [sshd]
    enabled = true
    port = ssh
    Logpath = %(sshd-log)s
    backend = systemd
    maxretry = 3
    findtime = 600
    bantime = 3600

- I figured out which configuration to use by checking Fail2Ban's jail.conf file after installation. It already had an SSH section, which made it super easy. Plus, it seemed like the only configuration needed for basic setup. Fail2Ban automatically adds 'iptables' rules to ban IPs without extra commands.
- logpath: This parameter tells Fail2Ban where to look for logs related to failed login attempts. %(sshd-log)s is a Fail2Ban variable that points to the system log file used for SSH login attempts.
    - How to find the exact log file on your system: <grep sshd /var/log/auth.log>
- backend: Setting this to systemd tells Fail2Ban to skip traditional log files and read directly from the systemd journal instead. Systemd is a system and service manager that uses systemctl to manage services.

--------------

### 2.) fail2ban-client status sshd
- Shows running jails and any banned IPs. This is useful letting me know that its working.
---------------

### 3.)<apt install iptables>
- Mandatory step: When I tried to start or enable Fail2Ban, I found that iptables was missing. This tool is essential for configuring the Linux kernel’s built-in firewall.
- iptables sets up rules to filter network traffic based on IP addresses, ports, protocols, and other network parameters.
- Fail2Ban has built-in commands to automatically use iptables to block IP addresses that show malicious behavior, such as repeated failed login attempts.
  
---------------

### 4.) fail2ban-client set sshd unbanip <IP_ADDR>

---------------
# Images
-[fail2ban-logs](https://github.com/AJprogramming123/Raspberry_Pi/tree/Main/Images/fail2ban-logs.png)
-[fail2ban](https://github.com/AJprogramming123/Raspberry_Pi/tree/Main/Images/fail2ban.png)
