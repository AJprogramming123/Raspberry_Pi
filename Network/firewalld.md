## firewalld Setup - (DROPS anything except: SSH, outgoing traffic, Samba)
I chose firewalld over ufw because it offers more granular control using zones and rich rules, making it better suited for managing complex firewall setups. It also integrates more cleanly with system services like Samba and supports dynamic configuration without needing to restart the firewall.

--------------------

## Commands:
- sudo firewall-cmd --zone=public --add-port=ssh/tcp --permanent
  - allows incoming SSH so in cant still manage the system remotely or login.
- sudo firewall-cmd --zone=public --add-service=samba --permanent
  - Opens the necessary Samba ports (137-139/UDP & TCP, 445/TCP) to allow file sharing across my local network
- sudo firewall-cmd --zone=public --add-masqueade --permanent
  - Enables NAT (Network Address Translation) for outgoing traffic. Essential for allowing the system to access the internet even though incoming ports are dropped. As long as i ask for incoming traffic myself first then theres no other way of accessing my system.
- sudo firewall-cmd --zone=public --set-target=DROP --permanent
  - sets the default behavior for the public zone to DROP all unmatched incoming packets. This is the actual part that locksdown the firewall completely.
- firewall-cmd --reload
  - This is for apply the changes.
  
