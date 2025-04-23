# jupyterhub_grouper_sync

jupyterhub_grouper_sync is a JupyterHub hub-managed service that syncs Jupyterhub users to grouper groups. 

## Configuration

jupyterhub_grouper_sync is configured through traitlets. Here is an example configuration:

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
