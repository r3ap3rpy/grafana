### API

The API allows you to accelerate and automate your grafana processes.

In order to use the API we need to have a user with  **Grafana Admin** access.

For example this curl command.

``` bash
curl -k https://localhost/api/admin/settings
```

Returns a message.

``` bash
{"message":"Unauthorized"}
```

Saying autorization is needed.

we can specify it like this for the curl command.

``` bash
curl -k https://localhost/api/admin/settings -u admin:admin
```

This returns a more detailed answer. But we are here for the python goodies. The above command returns the configuration of the server itself.