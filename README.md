# Install-Globus

## Install Server

https://docs.globus.org/globus-connect-server/v5.4/

Follow instructions here up to 

```
sudo globus-connect-server endpoint show

Display Name:    icarbon EDC Endpoint
ID:              bc07d979-fe9e-4d96-811c-9e04116df15c
Subscription ID: None
Public:          True
GCS Manager URL: https://eeca61.6fbd.data.globus.org
Network Use:     normal
Organization:    NC State Univ
Contact E-mail:  icarbon@ncsu.edu

```

Then start here
https://docs.globus.org/globus-connect-server/v5.4/data-access-guide/

```
globus-connect-server storage-gateway create posix "Gateway user galaxy" \
    --identity-mapping file:identity_map.json \
    --restrict-paths file:path-restrictions.json \
    --domain ncsu.edu
    
globus-connect-server storage-gateway list
Display Name        | ID                                   | Connector | High Assurance | MFA  
------------------- | ------------------------------------ | --------- | -------------- | -----
Gateway user galaxy | cf299ec6-5aa7-42f2-94a3-ce20ddee7c7e | POSIX     | False          | False

globus-connect-server collection create cf299ec6-5aa7-42f2-94a3-ce20ddee7c7e \
/icarbon_temp_10tb/database/files "Gateway user galaxy"

globus-connect-server collection list
ID                                   | Display Name        | Owner             | Collection Type | Storage Gateway ID                  
------------------------------------ | ------------------- | ----------------- | --------------- | ------------------------------------
2ee2a005-5c76-4e81-a866-2513dade1ca3 | Gateway user galaxy | jbwhite2@ncsu.edu | mapped          | cf299ec6-5aa7-42f2-94a3-ce20ddee7c7e

```

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
    "read_write": ["/icarbon_temp_10tb/database/files/$USER@ncsu.edu"]
}

```
useradd -u 58413 galaxy

## Install Auth app

https://docs.globus.org/api/auth/developer-guide/

https://galaxyproject.org/authnz/use/oidc/idps/globus/

https://galaxyproject.org/authnz/config/oidc/idps/globus/


