### Setup HTTP 

In order to run grafana on ports other than the default we need to first configure the **grafana.ini**

It is located in the **/etc/grafana/** folder.

You should replace the line.

``` bash
# The http port  to use
;http_port = 3000
```

With this.

``` bash
# The http port  to use
http_port = 80
```

Then we have two options, either use the **setcap** to grant binary permission.

``` bash
setcap 'cap_net_bind_service=+ep' /usr/sbin/grafana-server
```

Or use **iptables** to reroute the traffic between ports.

``` bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 3000
```

If you go with the latter case you don't need to modify the config.

Finally restart your **grafana-server** service.

``` bash
systemctl restart grafana-server
```