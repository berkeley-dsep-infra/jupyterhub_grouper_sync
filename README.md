# calgroup_builder

calgroup_builder is a JupyterHub hub-managed service that syncs DataHub users to Berkeley calgroups. 

## Configuration

calgroup_builder is configured through traitlets. Here is an example configuration:

```python

c.JupyterHub.services = [
    {
        'name': "calgroup-builder",
        'command': ["calgroup-sync", '--hub_name=dev', '--url=http://localhost:8081/hub/api', '--calgroup_base_url=https://calgroups.berkeley.edu/gws/servicesRest/json/v2_2_100', '--grouper_user={grouper user}', '--group_pass={grouper password}']
    }
]

c.JupyterHub.load_roles = [
    {
        "name": "calgroup-builder",
        "scopes": [
            "list:users",
            "read:users",
            "admin:auth_state",
        ],
        # assign the role to our service, so it gains these permissions
        "services": ["calgroup-builder"],
    }
]

```
