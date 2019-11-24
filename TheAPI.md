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

### Managing teams and users.

We initialize every one of our scripts the following way.

``` python
import requests
import json
from requests.auth import HTTPBasicAuth

credentials = HTTPBasicAuth('admin','Start!123')
```

Let's create a new user.

``` python
user_data = {
    "name":"test1",
  "email":"test",
  "login":"test1",
  "password":"Start!123"
}
requests.post(url = "https://centosa/api/admin/users", auth = credentials, verify = False, headers = {'Content-Type':'application/json'}, data = json.dumps(user_data)).text
```

Then in order to list our teams we do the following.

``` python
requests.get(url = "https://centosa/api/teams",auth = credentials, verify = False, headers = {'Content-Type': 'application/json'}).text
```

In order to list the members of our teams we do the following.

``` python
requests.get(url = "https://centosa/api/teams/2/members",auth = credentials, verify = False, headers = {'Content-Type': 'application/json'}).text
```

To create a new team we do the following.

``` python
team_info = {
  "name": "MyTestTeam",
  "email": "email@test.com"
}

requests.post(url = "https://centosa/api/teams", data = json.dumps(team_info) ,auth = credentials, verify = False, headers = {'Content-Type': 'application/json'}).text
```

To update the team we do the following.

``` python
team_info = {
  "name": "MyTestTeam",
  "email": "admins@test.com"
}
requests.put(url = "https://centosa/api/teams/2", data = json.dumps(team_info) ,auth = credentials, verify = False, headers = {'Content-Type': 'application/json'}).text
```

To add a new member to our team.

``` python
requests.post(url = "https://centosa/api/teams/2/members", data = json.dumps({'userId':1}) ,auth = credentials, verify = False, headers = {'Content-Type': 'application/json'}).text)
```

To remove a member from our team.

``` python
requests.delete(url = "https://centosa/api/teams/2/members/1", data = json.dumps({'userId':1}) ,auth = credentials, verify = False, headers = {'Content-Type': 'application/json'}).text
```

To delete a team.

``` python
requests.delete(url = "https://centosa/api/teams/2" ,auth = credentials, verify = False, headers = {'Content-Type': 'application/json'}).text
```
