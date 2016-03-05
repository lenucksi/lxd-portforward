# lxd-portforward

Simple script to automatically set up port forwarding for LXD containers. Inspired by
[evanhempel/lxc-portforward](//github.com/evanhempel/lxc-portforward).


## Usage

Copy `lxd-portforward`, `lxd-portforward-helper`, and `lxd-portforward.conf.template`
(renamed as `lxd-portforward.conf`) to `/etc/lxd`.

In your LXD container or profile config set:

```
raw.lxc: |-
  lxc.hook.post-stop = /etc/lxd/lxd-portforward
  lxc.hook.pre-start = /etc/lxd/lxd-portforward
```

Edit `lxd-portforward.conf` to forward the ports you want forwarded.


## Files

Port forwarding information is stored in `/etc/lxd/lxd-portforward.conf`. Format is:

```
<container_name>:<local_port>:<remote_port>
```

IP addresses are stored in `/var/run/lxd-portforward/<container name>` so when
the container is stopped the proper `iptables` rules can be removed.


## Author & Licence

© 2016 Sebastian Gröhn, licenced under the [MIT License](LICENCE.txt).
