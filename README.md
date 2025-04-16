# group_builder

group_builder is a JupyterHub hub-managed service that syncs Jupyterhub users to grouper groups. 

## Configuration

group_builder is configured through traitlets. Here is an example configuration:

```python

c.JupyterHub.services = [
    {
        'name': "group-builder",
        'command': ["group-sync",  '--url=http://localhost:8081/hub/api', '--group_base_url=https://calgroups.berkeley.edu/gws/servicesRest/json/v2_2_100', '--grouper_user={grouper user}', '--grouper_pass={grouper password}', '--group_name=edu:berkeley:app:datahub:datahub-dev-users']
    }
]

c.JupyterHub.load_roles = [
    {
        "name": "group-builder",
        "scopes": [
            "list:users",
            "read:users",
            "admin:auth_state",
        ],
        # assign the role to our service, so it gains these permissions
        "services": ["group-builder"],
    }
]

```
