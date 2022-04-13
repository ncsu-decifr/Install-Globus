# Install-Globus

## Install Server

https://docs.globus.org/globus-connect-server/v5.4/

identity_map.json
```
{
  "DATA_TYPE": "expression_identity_mapping#1.0.0",
  "mappings": [
    {
      "source": "{username}",
      "match": "(.*)ncsu\\.edu",
      "output": "galaxy"
    }
  ]
}
```

path-restrictions.json
```
{
    "DATA_TYPE": "path_restrictions#1.0.0",
    "read_write": ["$USER" + "@ncsu.edu"]
}
```

## Install Auth app

https://docs.globus.org/api/auth/developer-guide/

https://galaxyproject.org/authnz/use/oidc/idps/globus/

https://galaxyproject.org/authnz/config/oidc/idps/globus/


