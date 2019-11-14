### Firewall settings

Stopping and disabling the firewalld is NOT recommended. For testing it's okay, but after it goes to production we rather use this security feature.

In order to allow HTTP traffic you need to issue the following commands.

``` bash
firewall-cmd --zone=public --add-service=http
firewall-cmd --zone=public --add-service=http --permanent
```

In order to allow HTTPS traffic you need to issue thse commands.

``` bash
firewall-cmd --zone=public --add-service=https
firewall-cmd --zone=public --add-service=https --permanent
```

Note that if you only issue the second command you need to reload your service for the change to be applied that's why both are used.