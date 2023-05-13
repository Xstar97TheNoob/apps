# apps

my current truenas scale app across multiple nodes -> [my apps](./my-apps.md).

checkout the n8n [workflow](./truenas_app_list_generator_template.json) and upload it to your local n8n instance.

# prerequisites

- add this node [splitinbatches-advanced](https://www.npmjs.com/package/n8n-nodes-splitinbatches-advanced) to your n8n instance to use the workflow

- In scale go to the top right person settings -> api keys or http://truenas.local:81/ui/apikeys and create an api key to authenicate the scale api.
- Create a repo and add a empty markdown file (and call it whatever you like.) or use the README.md, the choice is yours.

# setup the get-config-data node

just edit the "get-config-data" node and replace the following fields in ALL CAPS.

the "scale_servers" is an json object array that will support multiple servers.

the "filter_list" is a string array of chart names that will be excluded from the list if you dont want them to be listed in the app-list.md
for example: ["n8n", "app1", "app2"]

manually run the workflow or activate it to run every 6hrs (change the cron node to whatever you want.)

```json

{
    "repo":{
        "repo_owner":"REPO_OWNER",
        "repo_name":"REPO_NAME",
        "app_list":"APP_LIST_FILE.md",
        "commit_msg":"update app list",
        "trains_info":{
            "dependency":{
                "name":"dependency",
                "description":"Contains charts that are mostly used as dependencies.",
                "emoji":"🔨"
            },
            "enterprise":{
                "name":"enterprise",
                "description":"WIP. Full details to be announced soon.",
                "emoji":"👔"
            },
            "stable":{
                "name":"stable",
                "description":"Contains most of our charts. These are considered stable and working.",
                "emoji":"✅"
            },
            "incubator":{
                "name":"incubator",
                "description":"These Charts are still in development and/or are not considered to be of high-enough quality.",
                "emoji":"⚠️"
            },
            "wip":{
                "name":"WIP",
                "description":"WIP.",
                "emoji":"👷"
            }
        }
    },
    "api":{
        "base":"/api/v2.0",
        "charts_release":"/chart/release"
    },
    "scale_servers":[
        {
            "url":"http://IP:PORT",
            "name":"NAME",
            "description":"DESCRIPTION",
            "token":"API_TOKEN"
        }
    ],
    "new_badge_emoji":"🆕",
    "max_days_new_badge":3,
    "image_size":{
        "width":48,
        "height":36
    },
    "catalogs":[
        "truecharts",
        "official"
    ],
    "filter_list":[
        ""
    ]
}

```
