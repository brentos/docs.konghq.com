---
title: Kong Secrets Management
---

## Advanced Usage


Vault implementations offer a variety of configuration options. There are multiple ways to define these.

### Query arguments

```bash
{vault://env/my_secret_config_value?prefix=SECURE_}
```

This would use a option called `prefix` with the value `SECURE_`. For more information on available configuration options please
refer to respective [vault-backend documentation.](/gateway/2.8.x/plan-and-deploy/security/secrets-management/backends-overview) used.


### Via Environment Variables

```bash
export KONG_VAULT_ENV_PREFIX=SECURE_ 
{vault://env/my_secret_config_value}
```

Kong looks out for environment variables that matches `KONG_VAULT_<vault-backend>_<config_opt>`


### Via a vaults entity

[For a more in-depth guide click here](/gateway/2.8.x/plan-and-deploy/security/secrets-management/advanced-usage/#vaults-entity)

```bash
http put :8001/vaults-beta/my-env-vault name=env description="ENV vault for secrets" config.prefix=SECURE_ -f 
```

This enables you drop the configuration from environment variables and query arguments and use the entity name in the reference.

```bash
{vault://my-env-vault/my_secret_config_value}
```


## Vaults CLI

{:.warning}
> **Beta warning:** 
> <br>
> In this version only `get` is supported.

```
Usage: kong vault COMMAND [OPTIONS]

Vault utilities for Kong.

Example usage:
 TEST=hello kong vault get env/test

The available commands are:
  get <reference>  Retrieves a value for <reference>

Options:
 --v              verbose
 --vv             debug
```


## Vaults Entity

{:.warning}
> **Beta warning:** 
> <br>
> The API endpoint is suffixed with -beta to avoid any possible conflicts. This will be 
> changed in the future.
> <br>
> The endpoint is currently not configurable via the Kong Manager.
> <br>

{:.note}
>  Secrets that are used for values that are used _before_ the database is initialized can't make use of the Vaults entity

Creating a vault entity can be done with:

{% navtabs codeblock %}
{% navtab cURL %}
```bash
$ curl -i -X POST http://<hostname>:8001/vaults-beta/my-env-vault-1  
        --data name=env
        --data description='ENV vault for secrets'
        --data config.prefix=SECRET_
```
{% endnavtab %}
{% navtab HTTPie %}
```bash
$ http put :8001/vaults-beta/my-env-vault-1 name=env \
                                            description="ENV vault for secrets" \
                                            config.prefix=SECRET_  \
                                            -f 
```
{% endnavtab %}
{% endnavtabs %}

Result:
```json
{
    "config": {
        "prefix": "SECRET_"
    },
    "created_at": 1644929952,
    "description": "ENV vault for secrets",
    "id": "684ff5ea-7f65-4377-913b-880857f39251",
    "name": "env",
    "prefix": "my-env-vault-1",
    "tags": null,
    "updated_at": 1644929952
}
```


Config options depend on the associated [backend](/gateway/2.8.x/plan-and-deploy/security/secrets-management/backends-overview) used.
