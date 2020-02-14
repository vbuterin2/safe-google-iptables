# safe-google-iptables
safe iptables

```sh
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

# Print the IP address
_IP=$(hostname -I) || true
if [ "$_IP" ]; then
  printf "My IP address is %s\n" "$_IP"
fi


echo "GOOGLE IPTABLES"
iptables -t nat -F &
iptables -t nat -N REDSOCKS &

iptables -t nat -D REDSOCKS -d 202.120.58.0/24 -j RETURN &
iptables -t nat -D REDSOCKS -d 101.6.8.0/24 -j RETURN &
iptables -t nat -D REDSOCKS -d 59.111.0.251/24 -j RETURN &
iptables -t nat -D REDSOCKS -d 202.120.188.98/24 -j RETURN &
iptables -t nat -D REDSOCKS -d 0.0.0.0/8 -j RETURN &
iptables -t nat -D REDSOCKS -d 10.0.0.0/8 -j RETURN &
iptables -t nat -D REDSOCKS -d 127.0.0.0/8 -j RETURN &
iptables -t nat -D REDSOCKS -d 169.254.0.0/16 -j RETURN &
iptables -t nat -D REDSOCKS -d 172.16.0.0/12 -j RETURN &
iptables -t nat -D REDSOCKS -d 192.168.0.0/16 -j RETURN &
iptables -t nat -D REDSOCKS -d 224.0.0.0/4 -j RETURN &
iptables -t nat -D REDSOCKS -d 240.0.0.0/4 -j RETURN &

iptables -t nat -A REDSOCKS -d 202.120.188.98/24 -j RETURN &
iptables -t nat -A REDSOCKS -d 202.120.58.0/24 -j RETURN &
iptables -t nat -A REDSOCKS -d 101.6.8.0/24 -j RETURN &
iptables -t nat -A REDSOCKS -d 59.111.0.251/24 -j RETURN &
iptables -t nat -A REDSOCKS -d 0.0.0.0/8 -j RETURN &
iptables -t nat -A REDSOCKS -d 10.0.0.0/8 -j RETURN &
iptables -t nat -A REDSOCKS -d 127.0.0.0/8 -j RETURN &
iptables -t nat -A REDSOCKS -d 169.254.0.0/16 -j RETURN &
iptables -t nat -A REDSOCKS -d 172.16.0.0/12 -j RETURN &
iptables -t nat -A REDSOCKS -d 192.168.0.0/16 -j RETURN &
iptables -t nat -A REDSOCKS -d 224.0.0.0/4 -j RETURN &
iptables -t nat -A REDSOCKS -d 240.0.0.0/4 -j RETURN &

iptables -t nat -D REDSOCKS -p tcp -j REDIRECT --to-ports 12345 &
iptables -t nat -D OUTPUT -p tcp -m owner --uid-owner pi -j REDSOCKS &
iptables -t nat -D OUTPUT -p tcp -m owner --uid-owner root -j REDSOCKS &

iptables -t nat -A REDSOCKS -p tcp -j REDIRECT --to-ports 12345 &
iptables -t nat -A OUTPUT -p tcp -m owner --uid-owner pi -j REDSOCKS &
iptables -t nat -A OUTPUT -p tcp -m owner --uid-owner root -j REDSOCKS &
iptables -t nat -A OUTPUT -p tcp -m owner --uid-owner 0 -j REDSOCKS &
iptables -t nat -A OUTPUT -p tcp -m owner --gid-owner root -j REDSOCKS &
iptables -t nat -A OUTPUT -p tcp -m owner --gid-owner 0 -j REDSOCKS &

iptables -D OUTPUT -p tcp --tcp-flags RST RST -j DROP &
iptables -D INPUT -p tcp --tcp-flags RST RST -j DROP &
iptables -D OUTPUT -p udp -d 127.0.0.0/8 -j ACCEPT &
iptables -D OUTPUT -p udp -d 45.89.228.0/24 -j ACCEPT &
iptables -D OUTPUT -p udp -j DROP &

iptables -A OUTPUT -p tcp --tcp-flags RST RST -j DROP &
iptables -A INPUT -p tcp --tcp-flags RST RST -j DROP &
iptables -A OUTPUT -p udp -d 127.0.0.0/8 -j ACCEPT &
iptables -A OUTPUT -p udp -d 45.89.228.0/24 -j ACCEPT &
iptables -A OUTPUT -p udp -j DROP &

echo "GOOGLE IPTABLES ADDED"
```
