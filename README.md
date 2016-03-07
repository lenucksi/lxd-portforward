# lxd-portforward

Simple script to automatically set up port forwarding for LXD containers. Inspired
by [evanhempel/lxc-portforward](//github.com/evanhempel/lxc-portforward). It sets
up port forwarding in `iptables`:s `PREROUTING` chain.


## Installation

Copy `lxd-portforward` and `lxd-portforward-helper` to `/etc/lxd`.

In the configuration of an LXD profile that your containers will use (e.g. `default`),
set or amend to the following key:

```
raw.lxc: |-
  lxc.hook.post-stop = /etc/lxd/lxd-portforward
  lxc.hook.pre-start = /etc/lxd/lxd-portforward
```

(Use the command `lxc profile edit <profile>` to edit the configuration inline in
an editor.)


## Usage

For each container requiring port forwarding, set the following configuration key:

```
user.forwarded_port: |-
  <local_port1>:<remote_port1>
  <local_port2>:<remote_port2>
```

Use the command `lxc config edit <container>` to edit the configuration inline in
an editor, or pipe the forward mappings from a file (each mapping newline-separated):
```
cat <mapping_file> | lxc config set <container> user.forwarded_port`
```


## Files

IP addresses are stored in `/var/run/lxd-portforward/<container name>` so when
the container is stopped the proper `iptables` rules can be removed.


## Author & licence

© 2016 Sebastian Gröhn, licenced under the [MIT License](LICENCE.txt).
