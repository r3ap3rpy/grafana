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

### Managing dashboards

Get a list of dashboards.

``` python
requests.get(url = "https://centosa/api/dashboards",verify = False, auth=credentials,headers = {'Content-Type':'application/json'}).text
```

Create a dashboard.

``` python
dbrd_data = {
  "dashboard": {
    "id": None,
    "uid": None,
    "title": "Production Overview",
    "tags": [ "templated" ],
    "timezone": "browser",
    "schemaVersion": 16,
    "version": 0
  },
  "folderId": 0,
  "overwrite": False
}
requests.post(url = "https://centosa/api/dashboards/db", data=json.dumps(dbrd_data),verify = False, auth=credentials,headers = {'Content-Type':'application/json'}).text
```

``` python
{
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": "-- Grafana --",
        "enable": True,
        "hide": True,
        "iconColor": "rgba(0, 211, 255, 1)",
        "name": "Annotations & Alerts",
        "type": "dashboard"
      }
    ]
  },
  "editable": True,
  "gnetId": None,
  "graphTooltip": 0,
  "id": 1,
  "links": [],
  "panels": [
    {
      "aliasColors": {},
      "bars": False,
      "dashLength": 10,
      "dashes": False,
      "datasource": None,
      "fill": 1,
      "fillGradient": 10,
      "gridPos": {
        "h": 8,
        "w": 24,
        "x": 0,
        "y": 0
      },
      "id": 4,
      "legend": {
        "avg": False,
        "current": False,
        "max": False,
        "min": False,
        "show": True,
        "total": False,
        "values": False
      },
      "lines": True,
      "linewidth": 1,
      "nullPointMode": "null",
      "options": {
        "dataLinks": []
      },
      "percentage": False,
      "pointradius": 2,
      "points": False,
      "renderer": "flot",
      "seriesOverrides": [],
      "spaceLength": 10,
      "stack": False,
      "steppedLine": False,
      "targets": [
        {
          "format": "table",
          "group": [],
          "metricColumn": "none",
          "rawQuery": True,
          "rawSql": """SELECT\n  \"TimeStamp\" AS \"time\",\n  \"Device\" AS \"\"\"Device\"\"\",\n  \"Availability\" AS \"\"\"Availability\"\"\"\nFROM \"Statistics\"\nWHERE\n  $__timeFilter(\"TimeStamp\")\n  AND\n  \"Device\" = 'DNS'\nGROUP BY \"Device\", \"Availability\", \"TimeStamp\"\nORDER BY 1\n""",
          "refId": "A",
          "select": [
            [
              {
                "params": [
                  "value"
                ],
                "type": "column"
              }
            ]
          ],
          "timeColumn": "time",
          "where": [
            {
              "name": "$__timeFilter",
              "params": [],
              "type": "macro"
            }
          ]
        }
      ],
      "thresholds": [
        {
          "colorMode": "critical",
          "fill": True,
          "line": True,
          "op": "lt",
          "value": 95,
          "yaxis": "left"
        }
      ],
      "timeFrom": None,
      "timeRegions": [],
      "timeShift": None,
      "title": "Availability for device: DNS",
      "tooltip": {
        "shared": True,
        "sort": 0,
        "value_type": "individual"
      },
      "transparent": True,
      "type": "graph",
      "xaxis": {
        "buckets": None,
        "mode": "time",
        "name": None,
        "show": True,
        "values": []
      },
      "yaxes": [
        {
          "format": "percent",
          "label": None,
          "logBase": 1,
          "max": None,
          "min": None,
          "show": True
        },
        {
          "format": "short",
          "label": None,
          "logBase": 1,
          "max": None,
          "min": None,
          "show": True
        }
      ],
      "yaxis": {
        "align": False,
        "alignLevel": None
      }
    },
    {
      "aliasColors": {},
      "bars": False,
      "dashLength": 10,
      "dashes": False,
      "datasource": None,
      "fill": 1,
      "fillGradient": 10,
      "gridPos": {
        "h": 9,
        "w": 24,
        "x": 0,
        "y": 8
      },
      "id": 2,
      "legend": {
        "avg": False,
        "current": False,
        "max": False,
        "min": False,
        "show": True,
        "total": False,
        "values": False
      },
      "lines": True,
      "linewidth": 1,
      "nullPointMode": "null",
      "options": {
        "dataLinks": []
      },
      "percentage": False,
      "pointradius": 2,
      "points": False,
      "renderer": "flot",
      "seriesOverrides": [],
      "spaceLength": 10,
      "stack": False,
      "steppedLine": False,
      "targets": [
        {
          "format": "table",
          "group": [],
          "metricColumn": "none",
          "rawQuery": True,
          "rawSql": """SELECT\n  \"TimeStamp\" AS \"time\",\n  \"Device\" AS \"\"\"Device\"\"\",\n  \"Availability\" AS \"\"\"Availability\"\"\"\nFROM \"Statistics\"\nWHERE\n  $__timeFilter(\"TimeStamp\")\n  AND\n  \"Device\" = 'DC'\nGROUP BY \"Device\", \"Availability\", \"TimeStamp\"\nORDER BY 1\n""",
          "refId": "A",
          "select": [
            [
              {
                "params": [
                  "value"
                ],
                "type": "column"
              }
            ]
          ],
          "timeColumn": "time",
          "where": [
            {
              "name": "$__timeFilter",
              "params": [],
              "type": "macro"
            }
          ]
        }
      ],
      "thresholds": [
        {
          "colorMode": "critical",
          "fill": True,
          "line": True,
          "op": "lt",
          "value": 99,
          "yaxis": "left"
        }
      ],
      "timeFrom": None,
      "timeRegions": [],
      "timeShift": None,
      "title": "Availability for device DC",
      "tooltip": {
        "shared": True,
        "sort": 0,
        "value_type": "individual"
      },
      "transparent": True,
      "type": "graph",
      "xaxis": {
        "buckets": None,
        "mode": "time",
        "name": None,
        "show": True,
        "values": []
      },
      "yaxes": [
        {
          "format": "percent",
          "label": None,
          "logBase": 1,
          "max": None,
          "min": None,
          "show": True
        },
        {
          "format": "short",
          "label": None,
          "logBase": 1,
          "max": None,
          "min": None,
          "show": True
        }
      ],
      "yaxis": {
        "align": False,
        "alignLevel": None
      }
    }
  ],
  "schemaVersion": 20,
  "style": "dark",
  "tags": [],
  "templating": {
    "list": []
  },
  "time": {
    "from": "now-30d",
    "to": "now"
  },
  "timepicker": {
    "refresh_intervals": [
      "5s",
      "10s",
      "30s",
      "1m",
      "5m",
      "15m",
      "30m",
      "1h",
      "2h",
      "1d"
    ]
  },
  "timezone": "",
  "title": "WahttttAvailability",
  "uid": "7cn47JbWz",
  "version": 1
}
```