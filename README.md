# jupyterhub_grouper_sync

jupyterhub_grouper_sync is a JupyterHub hub-managed service that syncs Jupyterhub users to grouper groups. 

## Configuration

jupyterhub_grouper_sync is configured via traitlets. The service can be configured either through command-line arguments or environment variables. 

Below is an example of how to configure the jupyterhub_grouper_sync service using command-line arguments:

```python

c.JupyterHub.services = [
    {
        'name': "grouper-sync",
        'command': ["grouper-sync",  '--url=http://localhost:8081/hub/api', '--grouper_base_url=https://calgroups.berkeley.edu/gws/servicesRest/json/v2_2_100', '--grouper_user={grouper user}', '--grouper_pass={grouper password}', '--grouper_id_path=edu:berkeley:app:datahub:datahub-dev-users']
    }
]

c.JupyterHub.load_roles = [
    {
        "name": "grouper-sync",
        "scopes": [
            "list:users",
            "read:users",
            "admin:auth_state",
        ],
        # assign the role to our service, so it gains these permissions
        "services": ["grouper-sync"],
    }
]

```
### Argument Descriptions

- `--url`: URL of the JupyterHub API.
- `--grouper_base_url`: Base URL of the Grouper REST API.
- `--grouper_user`: Username for authenticating with Grouper.
- `--grouper_pass`: Password for Grouper authentication.
- `--grouper_id_path`: Grouper group path to sync with.


Alternatively, the service can be configured by setting the following environment variables:

- `JUPYTERHUB_API_URL`
- `GROUPER_BASE_URL`
- `GROUPER_USER`
- `GROUPER_PASSWORD`
- `GROUPER_ID_PATH`
