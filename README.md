# lxd-portforward

Simple script to automatically set up port forwarding for LXD containers. Inspired by
[evanhempel/lxc-portforward](//github.com/evanhempel/lxc-portforward).


## Usage

Copy `lxd-portforward`, `lxd-portforward.conf`, and `lxd-portforward-helper` to `/etc/lxd`.

In your container config set:

    lxc.network.script.up = /etc/lxd/lxd-portforward
    lxc.network.script.down = /etc/lxd/lxd-portforward

Edit `lxd-portforward.conf` to forward the ports you want forwarded.


## Files

Port forwarding information is stored in `/etc/lxd/lxd-portforward.conf`. Format is:

```
container_name:local_port:remote_port
```

IP addresses are stored in `/var/run/lxd-portforward/<container name>` so when
the container is stopped the proper iptables rules can be removed.


## Author & Licence

© 2016 Sebastian Gröhn, licenced under the [MIT License](LICENCE.txt).
